# Git - Distributed Version Control System

Git is a fast, scalable distributed revision control system designed to handle everything from small to very large projects with speed and efficiency. Originally created by Linus Torvalds in 2005 for Linux kernel development, Git has become the de facto standard for version control in software development. The system tracks changes to files over time, enabling multiple developers to collaborate on projects, manage branches, merge changes, and maintain a complete history of all modifications.

Git's architecture is built around a content-addressable filesystem with immutable objects stored using cryptographic hashes (SHA-1 or SHA-256). The core design includes four fundamental object types: blobs (file contents), trees (directory structures), commits (snapshots with metadata), and tags (named references). This robust foundation supports distributed workflows where every repository contains the complete project history, eliminating single points of failure and enabling offline work. Git's efficient delta compression, packfile format, and sophisticated merge algorithms make it exceptionally fast even with large repositories containing millions of commits.

## Core APIs and Functions

### Command Registration and Dispatch

Built-in commands are registered through a command table that maps command names to handler functions with associated flags controlling execution behavior.

```c
// git.c - Command structure and registration
#include "builtin.h"
#include "repository.h"

#define RUN_SETUP        (1<<0)  // Requires git repository
#define RUN_SETUP_GENTLY (1<<1)  // Optionally works in repository
#define USE_PAGER        (1<<2)  // Auto-paginate output
#define NEED_WORK_TREE   (1<<3)  // Requires working tree
#define DELAY_PAGER_CONFIG (1<<4) // Defer pager configuration
#define NO_PARSEOPT      (1<<5)  // Manual option parsing

struct cmd_struct {
    const char *cmd;
    int (*fn)(int, const char **, const char *, struct repository *);
    unsigned int option;
};

// Example: Implementing a built-in command
int cmd_mystatus(int argc, const char **argv, const char *prefix,
                 struct repository *repo) {
    struct index_state *index = repo->index;

    // Parse options
    if (argc > 1 && !strcmp(argv[1], "--help")) {
        printf("Usage: git mystatus [options]\n");
        return 0;
    }

    // Access repository index
    if (repo_read_index(repo) < 0) {
        die("Failed to read index");
    }

    printf("Repository has %u entries in index\n", index->cache_nr);
    return 0;
}

// Register in commands[] table in git.c:
// { "mystatus", cmd_mystatus, RUN_SETUP }
```

### Repository Initialization and Access

The repository structure encapsulates all state for a Git repository including object database, references, configuration, and index.

```c
// repository.h - Core repository abstraction
#include "repository.h"
#include "config.h"
#include "object-file.h"

struct repository {
    char *gitdir;                      // Path to .git directory
    char *commondir;                   // Shared directory for worktrees
    struct object_database *objects;   // Object storage
    struct ref_store *refs_private;    // Reference store
    struct index_state *index;         // Staging area
    struct config_set *config;         // Configuration
    struct parsed_object_pool *parsed_objects; // Object cache
    const struct git_hash_algo *hash_algo;     // SHA-1 or SHA-256
};

// Example: Opening and using a repository
#include "setup.h"

int my_command(int argc, const char **argv, const char *prefix,
               struct repository *repo) {
    struct strbuf path = STRBUF_INIT;
    int ret;

    // Repository is already initialized by git.c infrastructure
    // Access git directory path
    printf("Git directory: %s\n", repo->gitdir);
    printf("Working tree: %s\n", repo->worktree);

    // Build path relative to repository
    strbuf_addf(&path, "%s/config", repo->gitdir);
    printf("Config file: %s\n", path.buf);

    // Check if repository uses reftable
    if (repo->ref_storage_format == REF_STORAGE_FORMAT_REFTABLE) {
        printf("Using reftable reference storage\n");
    } else {
        printf("Using files reference storage\n");
    }

    strbuf_release(&path);
    return 0;
}
```

### Object Database Operations

The object database manages reading and writing Git objects (blobs, trees, commits, tags) from loose files and packfiles.

```c
// odb.h - Object database operations
#include "odb.h"
#include "object.h"
#include "hex.h"

struct object_database {
    struct repository *repo;
    struct odb_source *sources;        // Primary + alternates
    struct oidmap replace_map;         // Object replacements
    struct packfile_store *packfiles;  // Pack management
    unsigned long approximate_object_count;
};

// Example: Reading object data
int read_object_example(struct repository *repo, const char *sha_hex) {
    struct object_id oid;
    enum object_type type;
    unsigned long size;
    void *content;
    int ret = 0;

    // Parse hex string to object ID
    if (get_oid_hex(sha_hex, &oid) < 0) {
        fprintf(stderr, "Invalid object ID: %s\n", sha_hex);
        return -1;
    }

    // Read object from database
    content = repo_read_object_file(repo, &oid, &type, &size);
    if (!content) {
        fprintf(stderr, "Object not found: %s\n", sha_hex);
        return -1;
    }

    // Process based on type
    switch (type) {
    case OBJ_COMMIT:
        printf("Commit object, size: %lu bytes\n", size);
        printf("Content:\n%.*s\n", (int)size, (char *)content);
        break;
    case OBJ_TREE:
        printf("Tree object, size: %lu bytes\n", size);
        break;
    case OBJ_BLOB:
        printf("Blob object, size: %lu bytes\n", size);
        break;
    case OBJ_TAG:
        printf("Tag object, size: %lu bytes\n", size);
        break;
    default:
        fprintf(stderr, "Unknown object type: %d\n", type);
        ret = -1;
    }

    free(content);
    return ret;
}

// Example: Writing a blob object
int write_blob_example(struct repository *repo, const char *data,
                       size_t len, struct object_id *oid_out) {
    // Write blob and get its OID
    if (write_object_file(data, len, OBJ_BLOB, oid_out) < 0) {
        fprintf(stderr, "Failed to write blob object\n");
        return -1;
    }

    char hex[GIT_MAX_HEXSZ + 1];
    printf("Created blob: %s\n", oid_to_hex_r(hex, oid_out));
    return 0;
}
```

### Reference Management

The references system provides atomic operations for reading, creating, updating, and deleting refs using transactions.

```c
// refs.h - Reference operations
#include "refs.h"
#include "object-id.h"

// Example: Reading a reference
int read_ref_example(struct repository *repo, const char *refname) {
    struct object_id oid;
    int flags = 0;
    const char *resolved;
    char hex[GIT_MAX_HEXSZ + 1];

    // Resolve reference (follows symbolic refs)
    struct ref_store *refs = get_main_ref_store(repo);
    resolved = refs_resolve_ref_unsafe(refs, refname,
                                       RESOLVE_REF_READING,
                                       &oid, &flags);

    if (!resolved) {
        fprintf(stderr, "Reference not found: %s\n", refname);
        return -1;
    }

    printf("Reference: %s\n", refname);
    printf("Resolved to: %s\n", resolved);
    printf("Object ID: %s\n", oid_to_hex_r(hex, &oid));

    if (flags & REF_ISSYMREF) {
        printf("Type: symbolic reference\n");
    } else {
        printf("Type: direct reference\n");
    }

    if (flags & REF_ISPACKED) {
        printf("Storage: packed-refs\n");
    }

    return 0;
}

// Example: Atomic reference update transaction
int update_ref_example(struct repository *repo, const char *refname,
                       const struct object_id *new_oid,
                       const struct object_id *old_oid) {
    struct ref_store *refs = get_main_ref_store(repo);
    struct ref_transaction *transaction;
    struct strbuf err = STRBUF_INIT;
    int ret = 0;

    // Create transaction
    transaction = ref_store_transaction_begin(refs, &err);
    if (!transaction) {
        fprintf(stderr, "Transaction begin failed: %s\n", err.buf);
        strbuf_release(&err);
        return -1;
    }

    // Add update to transaction with expected old value
    if (ref_transaction_update(transaction, refname, new_oid, old_oid,
                               NULL, NULL,
                               REF_NO_DEREF, // Don't follow symrefs
                               "update via API", // Reflog message
                               &err)) {
        fprintf(stderr, "Transaction update failed: %s\n", err.buf);
        ret = -1;
        goto cleanup;
    }

    // Commit transaction (atomic operation)
    if (ref_transaction_commit(transaction, &err)) {
        fprintf(stderr, "Transaction commit failed: %s\n", err.buf);
        ret = -1;
        goto cleanup;
    }

    printf("Successfully updated %s\n", refname);

cleanup:
    ref_transaction_free(transaction);
    strbuf_release(&err);
    return ret;
}

// Example: Iterating over all references
struct ref_cb_data {
    struct repository *repo;
    int count;
};

int ref_callback(const char *refname, const struct object_id *oid,
                 int flags, void *cb_data) {
    struct ref_cb_data *data = cb_data;
    char hex[GIT_MAX_HEXSZ + 1];

    printf("  %s -> %s", refname, oid_to_hex_r(hex, oid));
    if (flags & REF_ISSYMREF) {
        printf(" (symbolic)");
    }
    printf("\n");

    data->count++;
    return 0; // 0 = continue iteration, non-zero = stop
}

int list_refs_example(struct repository *repo) {
    struct ref_cb_data data = { .repo = repo, .count = 0 };
    struct ref_store *refs = get_main_ref_store(repo);

    printf("All references:\n");
    refs_for_each_ref(refs, ref_callback, &data);

    printf("\nTotal references: %d\n", data.count);
    return 0;
}
```

### Commit Object Manipulation

Working with commit objects including parsing, creating, and traversing commit history.

```c
// commit.h - Commit operations
#include "commit.h"
#include "object.h"
#include "strbuf.h"

struct commit {
    struct object object;
    timestamp_t date;
    struct commit_list *parents;
    struct tree *maybe_tree;
    unsigned int index;
};

// Example: Reading and parsing a commit
int parse_commit_example(struct repository *repo, const char *commitish) {
    struct object_id oid;
    struct commit *commit;
    const char *buffer;
    unsigned long size;

    // Look up commit by name (branch, tag, SHA)
    if (repo_get_oid(repo, commitish, &oid) < 0) {
        fprintf(stderr, "Invalid commit: %s\n", commitish);
        return -1;
    }

    commit = lookup_commit(repo, &oid);
    if (!commit) {
        fprintf(stderr, "Not a commit object\n");
        return -1;
    }

    // Parse commit data
    if (repo_parse_commit(repo, commit) < 0) {
        fprintf(stderr, "Failed to parse commit\n");
        return -1;
    }

    // Access commit properties
    printf("Commit: %s\n", oid_to_hex(&commit->object.oid));
    printf("Date: %lu\n", (unsigned long)commit->date);

    // Get commit message
    buffer = repo_get_commit_buffer(repo, commit, &size);
    if (buffer) {
        const char *msg = strstr(buffer, "\n\n");
        if (msg) {
            msg += 2; // Skip \n\n
            printf("Message: %s\n", msg);
        }
        repo_unuse_commit_buffer(repo, commit, buffer);
    }

    // Traverse parents
    struct commit_list *parents = commit->parents;
    printf("Parents:\n");
    while (parents) {
        printf("  %s\n", oid_to_hex(&parents->item->object.oid));
        parents = parents->next;
    }

    return 0;
}

// Example: Creating a new commit
int create_commit_example(struct repository *repo,
                         const struct object_id *tree_oid,
                         const struct commit_list *parents,
                         const char *author,
                         const char *committer,
                         const char *message,
                         struct object_id *commit_oid) {
    struct strbuf buffer = STRBUF_INIT;
    struct commit_list *p;

    // Build commit object
    strbuf_addf(&buffer, "tree %s\n", oid_to_hex(tree_oid));

    for (p = (struct commit_list *)parents; p; p = p->next) {
        strbuf_addf(&buffer, "parent %s\n",
                    oid_to_hex(&p->item->object.oid));
    }

    strbuf_addf(&buffer, "author %s\n", author);
    strbuf_addf(&buffer, "committer %s\n", committer);
    strbuf_addch(&buffer, '\n');
    strbuf_addstr(&buffer, message);

    // Write commit object
    if (write_object_file(buffer.buf, buffer.len, OBJ_COMMIT,
                         commit_oid) < 0) {
        fprintf(stderr, "Failed to write commit object\n");
        strbuf_release(&buffer);
        return -1;
    }

    printf("Created commit: %s\n", oid_to_hex(commit_oid));
    strbuf_release(&buffer);
    return 0;
}
```

### Configuration Management

Reading and writing Git configuration values across different scopes (system, global, local, worktree).

```c
// config.h - Configuration API
#include "config.h"
#include "repository.h"

enum config_scope {
    CONFIG_SCOPE_UNKNOWN = 0,
    CONFIG_SCOPE_SYSTEM,   // /etc/gitconfig
    CONFIG_SCOPE_GLOBAL,   // ~/.gitconfig
    CONFIG_SCOPE_LOCAL,    // .git/config
    CONFIG_SCOPE_WORKTREE, // .git/config.worktree
    CONFIG_SCOPE_COMMAND,  // -c command line
};

// Example: Reading configuration values
int read_config_example(struct repository *repo) {
    const char *value;
    int intval;

    // Read string value
    if (repo_config_get_string_tmp(repo, "user.name", &value) == 0) {
        printf("User name: %s\n", value);
    } else {
        printf("User name not configured\n");
    }

    // Read boolean value
    int boolval;
    if (repo_config_get_bool(repo, "core.bare", &boolval) == 0) {
        printf("Repository is %s\n", boolval ? "bare" : "not bare");
    }

    // Read integer value
    if (repo_config_get_int(repo, "core.compression", &intval) == 0) {
        printf("Compression level: %d\n", intval);
    }

    return 0;
}

// Example: Configuration callback for iteration
int config_callback(const char *key, const char *value,
                   const struct config_context *ctx, void *data) {
    int *count = data;

    printf("Config: %s = %s", key, value ? value : "(null)");

    if (ctx->kvi) {
        printf(" [scope: %s]", config_scope_name(ctx->kvi->scope));
    }
    printf("\n");

    (*count)++;
    return 0;
}

int iterate_config_example(struct repository *repo) {
    int count = 0;

    printf("All configuration:\n");
    repo_config(repo, config_callback, &count);
    printf("Total entries: %d\n", count);

    return 0;
}

// Example: Writing configuration
int write_config_example(struct repository *repo) {
    int ret;

    // Set a string value in local config
    ret = repo_config_set(repo, "section.key", "value");
    if (ret < 0) {
        fprintf(stderr, "Failed to set config: %d\n", ret);
        return -1;
    }

    // Set multiple values (creates multi-valued key)
    ret = repo_config_set_multivar(repo, "remote.origin.fetch",
                                   "^refs/heads/",
                                   "+refs/heads/*:refs/remotes/origin/*");
    if (ret < 0) {
        fprintf(stderr, "Failed to set multivar: %d\n", ret);
        return -1;
    }

    // Unset a value
    ret = repo_config_set(repo, "section.oldkey", NULL);

    printf("Configuration updated\n");
    return 0;
}
```

### Index (Staging Area) Operations

The index (staging area) tracks file states and prepares content for commits.

```c
// read-cache.h - Index operations
#include "read-cache-ll.h"
#include "cache-tree.h"

struct index_state {
    struct cache_entry **cache;
    unsigned int cache_nr;       // Number of entries
    unsigned int cache_alloc;    // Allocated size
    struct cache_tree *cache_tree; // Tree cache
    struct untracked_cache *untracked; // Untracked cache
    time_t timestamp;
};

struct cache_entry {
    struct stat_data ce_stat_data;
    struct object_id oid;
    unsigned int ce_mode;
    unsigned int ce_flags;
    unsigned int ce_namelen;
    char name[FLEX_ARRAY];
};

// Example: Reading and examining the index
int read_index_example(struct repository *repo) {
    struct index_state *index = repo->index;

    // Read index from disk
    if (repo_read_index(repo) < 0) {
        fprintf(stderr, "Failed to read index\n");
        return -1;
    }

    printf("Index contains %u entries:\n", index->cache_nr);

    // Iterate over all entries
    for (unsigned int i = 0; i < index->cache_nr; i++) {
        struct cache_entry *ce = index->cache[i];
        char hex[GIT_MAX_HEXSZ + 1];

        printf("  %s %06o %s\n",
               oid_to_hex_r(hex, &ce->oid),
               ce->ce_mode,
               ce->name);

        // Check entry flags
        if (ce->ce_flags & CE_VALID) {
            printf("    (valid)\n");
        }
        if (ce->ce_flags & CE_SKIP_WORKTREE) {
            printf("    (skip-worktree)\n");
        }

        // Stage number (0 = normal, 1-3 = conflict stages)
        int stage = ce_stage(ce);
        if (stage > 0) {
            printf("    (conflict stage %d)\n", stage);
        }
    }

    return 0;
}

// Example: Adding a file to the index
int add_to_index_example(struct repository *repo, const char *path) {
    struct index_state *index = repo->index;
    struct cache_entry *ce;
    struct stat st;

    // Stat the file
    if (lstat(path, &st) < 0) {
        fprintf(stderr, "Cannot stat %s: %s\n", path, strerror(errno));
        return -1;
    }

    // Hash the file and create cache entry
    if (add_to_index(index, path, &st, 0) < 0) {
        fprintf(stderr, "Failed to add %s to index\n", path);
        return -1;
    }

    // Write index back to disk
    if (write_locked_index(index, &lock_file, COMMIT_LOCK) < 0) {
        fprintf(stderr, "Failed to write index\n");
        return -1;
    }

    printf("Added %s to index\n", path);
    return 0;
}
```

### String Buffer Utilities

Dynamic string buffers for safe string manipulation.

```c
// strbuf.h - String buffer operations
#include "strbuf.h"

struct strbuf {
    size_t alloc;  // Allocated size
    size_t len;    // Current length
    char *buf;     // Buffer (always NUL-terminated)
};

#define STRBUF_INIT { .buf = strbuf_slopbuf }

// Example: Building strings with strbuf
int strbuf_example(void) {
    struct strbuf sb = STRBUF_INIT;
    struct object_id oid;

    // Initialize with capacity hint
    strbuf_init(&sb, 256);

    // Append various types
    strbuf_addstr(&sb, "commit ");

    // Formatted append
    get_oid("HEAD", &oid);
    strbuf_addstr(&sb, oid_to_hex(&oid));
    strbuf_addch(&sb, '\n');

    // Printf-style formatting
    strbuf_addf(&sb, "Author: %s <%s>\n", "John Doe", "john@example.com");

    // Read from file
    if (strbuf_read_file(&sb, ".git/description", 0) < 0) {
        fprintf(stderr, "Cannot read description\n");
    }

    // Trim whitespace
    strbuf_trim(&sb);

    // Use the string
    printf("Result:\n%s\n", sb.buf);
    printf("Length: %zu bytes\n", sb.len);

    // Clean up
    strbuf_release(&sb);
    return 0;
}

// Example: String manipulation
void strbuf_manipulation_example(void) {
    struct strbuf path = STRBUF_INIT;

    // Build path components
    strbuf_addstr(&path, "/home/user");
    strbuf_addch(&path, '/');
    strbuf_addstr(&path, "project");

    // Make relative
    strbuf_remove(&path, 0, 1); // Remove leading /

    // Replace substring
    strbuf_replace(&path, "user", 4, "developer", 9);

    // Insert at position
    strbuf_insert(&path, 0, "./", 2);

    printf("Path: %s\n", path.buf); // "./home/developer/project"

    strbuf_release(&path);
}
```

## Summary and Integration

Git's internal APIs provide a comprehensive framework for version control operations, from low-level object storage to high-level branch and commit management. The main use cases include building custom Git commands (via the builtin command infrastructure), implementing Git-aware tools (using the object database and reference APIs), creating repository analysis utilities (traversing commits and refs), and developing custom merge or diff tools (leveraging the tree and blob APIs). These APIs enable developers to extend Git's functionality while maintaining consistency with Git's core design principles.

Integration patterns typically involve initializing a repository structure through the setup functions, performing operations using the appropriate subsystem APIs (objects, refs, index, config), and leveraging utility libraries like strbuf for safe string handling. The transactional nature of reference updates ensures atomicity, while the object database's content-addressable design guarantees data integrity. Commands follow a standard lifecycle: option parsing (using parse-options API), repository access (via the repository structure), core logic implementation (using subsystem APIs), and cleanup. Error handling uses standard return codes with descriptive error messages, and the trace2 API provides observability for performance analysis and debugging.
