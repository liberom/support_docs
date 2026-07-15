# Ansible Core

Ansible is a radically simple IT automation platform that makes applications and systems easier to deploy and maintain. It automates software provisioning, configuration management, application deployment, orchestration, and many other IT processes without requiring agents on managed nodes. Ansible uses simple YAML-based playbooks to describe automation jobs, connecting to remote machines over SSH (or WinRM for Windows) and executing tasks using Python modules that run on the target hosts.

The core engine (ansible-core) provides the fundamental automation framework including the playbook executor, module system, inventory management, variable handling, templating with Jinja2, and the plugin architecture. It includes essential built-in modules for file management, package installation, service control, user administration, and command execution. Ansible follows a push-based model where control nodes execute tasks on managed nodes without requiring persistent daemons, making it lightweight and secure by design.

## Command Line Interface

### ansible-playbook - Execute Automation Playbooks

The `ansible-playbook` command executes one or more Ansible playbooks against inventory hosts. Playbooks are YAML files containing ordered lists of tasks (plays) that define the desired state of managed systems. The command supports check mode for dry runs, diff mode for showing changes, and various verbosity levels for debugging.

```bash
# Run a playbook against default inventory
ansible-playbook site.yml

# Run with specific inventory and limit to certain hosts
ansible-playbook -i inventory/production site.yml --limit webservers

# Run in check mode (dry run) with diff output
ansible-playbook site.yml --check --diff

# Run with extra variables passed at runtime
ansible-playbook deploy.yml -e "version=1.2.3 environment=staging"

# Run with increased verbosity for debugging
ansible-playbook site.yml -vvv

# Run specific tags only
ansible-playbook site.yml --tags "configuration,packages"

# Skip specific tags
ansible-playbook site.yml --skip-tags "notification"

# Start at a specific task
ansible-playbook site.yml --start-at-task "Install nginx"

# Run with vault password for encrypted files
ansible-playbook site.yml --ask-vault-pass
# Or using a password file
ansible-playbook site.yml --vault-password-file ~/.vault_pass
```

### ansible - Ad-Hoc Command Execution

The `ansible` command runs single tasks (ad-hoc commands) against inventory hosts without writing a playbook. Useful for quick one-off tasks, system checks, and interactive operations. Supports all core modules and allows parallel execution across multiple hosts.

```bash
# Ping all hosts to verify connectivity
ansible all -m ping

# Run a shell command on all webservers
ansible webservers -m shell -a "uptime"

# Copy a file to all hosts
ansible all -m copy -a "src=/local/file.txt dest=/remote/file.txt mode=0644"

# Install a package on Debian-based systems
ansible webservers -m apt -a "name=nginx state=present" --become

# Restart a service
ansible webservers -m service -a "name=nginx state=restarted" --become

# Gather facts from hosts
ansible all -m setup

# Gather specific facts only
ansible all -m setup -a "filter=ansible_distribution*"

# Run with specific inventory
ansible -i inventory/staging all -m ping

# Run against specific host pattern
ansible "web*.example.com" -m ping

# Run with sudo/become
ansible all -m command -a "cat /etc/shadow" --become --become-user=root
```

### ansible-vault - Secrets Management

The `ansible-vault` command manages encrypted files containing sensitive data such as passwords, API keys, and certificates. Vault-encrypted files can be used directly in playbooks and are decrypted automatically during execution. Supports multiple vault IDs for different security contexts.

```bash
# Create a new encrypted file
ansible-vault create secrets.yml

# Edit an encrypted file
ansible-vault edit secrets.yml

# Encrypt an existing file
ansible-vault encrypt vars/credentials.yml

# Decrypt a file (permanently)
ansible-vault decrypt vars/credentials.yml

# View encrypted file contents
ansible-vault view secrets.yml

# Re-encrypt with a new password
ansible-vault rekey secrets.yml

# Encrypt a string for embedding in YAML
ansible-vault encrypt_string 'supersecretpassword' --name 'db_password'
# Output can be embedded directly in playbooks:
# db_password: !vault |
#   $ANSIBLE_VAULT;1.1;AES256
#   ...encrypted data...

# Use multiple vault IDs
ansible-vault create --vault-id dev@prompt secrets_dev.yml
ansible-vault create --vault-id prod@~/.vault_prod secrets_prod.yml

# Run playbook with multiple vault passwords
ansible-playbook site.yml --vault-id dev@prompt --vault-id prod@~/.vault_prod
```

### ansible-galaxy - Role and Collection Management

The `ansible-galaxy` command installs, creates, and manages Ansible roles and collections from Galaxy (community repository) or private sources. Collections bundle multiple roles, modules, plugins, and playbooks into distributable packages with dependency management.

```bash
# Install a role from Galaxy
ansible-galaxy role install geerlingguy.nginx

# Install a specific version of a role
ansible-galaxy role install geerlingguy.docker,6.1.0

# Install roles from a requirements file
ansible-galaxy role install -r requirements.yml
# requirements.yml example:
# roles:
#   - name: geerlingguy.nginx
#   - name: geerlingguy.docker
#     version: "6.1.0"
#   - src: https://github.com/user/role.git
#     version: main
#     name: custom_role

# Install a collection
ansible-galaxy collection install community.general

# Install collections from requirements
ansible-galaxy collection install -r requirements.yml
# requirements.yml example:
# collections:
#   - name: community.general
#     version: ">=5.0.0"
#   - name: ansible.posix

# Create a new role scaffold
ansible-galaxy role init my_new_role

# Create a new collection scaffold
ansible-galaxy collection init my_namespace.my_collection

# List installed roles
ansible-galaxy role list

# List installed collections
ansible-galaxy collection list

# Install from a private Galaxy server
ansible-galaxy collection install my_namespace.my_collection --server https://galaxy.example.com
```

### ansible-inventory - Inventory Inspection

The `ansible-inventory` command displays or dumps the configured inventory in various formats. Useful for debugging inventory scripts, verifying host groupings, and exporting inventory data for other tools.

```bash
# Display inventory as a graph
ansible-inventory --graph

# Display inventory as JSON
ansible-inventory --list

# Show specific host's variables
ansible-inventory --host webserver1

# Display inventory with all variables
ansible-inventory --list --yaml

# Use specific inventory file
ansible-inventory -i inventory/production --graph

# Export inventory to file
ansible-inventory --list --output inventory.json

# Show inventory graph with variables
ansible-inventory --graph --vars
```

## Core Modules

### ansible.builtin.command - Execute Commands

Executes commands on remote nodes without shell processing. The command is not run through a shell, so variables like `$HOME` and operations like `<`, `>`, `|`, `;` and `&` will not work. Use the `shell` module for shell features. This module is safer for executing commands with user input as it avoids shell injection vulnerabilities.

```yaml
# Execute a simple command
- name: Check disk usage
  ansible.builtin.command: df -h
  register: disk_usage

- name: Display disk usage
  ansible.builtin.debug:
    var: disk_usage.stdout_lines

# Execute command with arguments as list (safer)
- name: Create a directory
  ansible.builtin.command:
    argv:
      - mkdir
      - -p
      - /opt/myapp/data

# Execute command with working directory
- name: Run make in project directory
  ansible.builtin.command:
    cmd: make install
    chdir: /opt/myproject

# Execute only if a file doesn't exist (idempotent)
- name: Initialize database
  ansible.builtin.command:
    cmd: /opt/myapp/bin/init-db.sh
    creates: /var/lib/myapp/database.db

# Execute only if a file exists
- name: Run migration only if needed
  ansible.builtin.command:
    cmd: /opt/myapp/bin/migrate.sh
    removes: /var/lib/myapp/pending_migrations

# Capture command output with error handling
- name: Get application version
  ansible.builtin.command: /opt/myapp/bin/version
  register: app_version
  changed_when: false
  failed_when: app_version.rc != 0

- name: Display version
  ansible.builtin.debug:
    msg: "Application version: {{ app_version.stdout }}"
```

### ansible.builtin.shell - Execute Shell Commands

Executes commands through a shell (`/bin/sh`) on remote nodes. Supports shell features like pipes, redirects, environment variables, and glob patterns. Use when shell processing is required; otherwise prefer the `command` module for security.

```yaml
# Execute command with shell features
- name: Find and count log files
  ansible.builtin.shell: find /var/log -name "*.log" | wc -l
  register: log_count

# Use environment variables
- name: Run with custom environment
  ansible.builtin.shell: echo $MY_VAR
  environment:
    MY_VAR: "hello world"

# Use pipes and redirects
- name: Process and save output
  ansible.builtin.shell: |
    cat /var/log/syslog | grep ERROR | tail -100 > /tmp/recent_errors.txt

# Execute multi-line script
- name: Complex shell operations
  ansible.builtin.shell: |
    set -e
    cd /opt/myapp
    ./configure --prefix=/usr/local
    make -j$(nproc)
    make install
  args:
    executable: /bin/bash

# Use different shell
- name: Run with specific shell
  ansible.builtin.shell: source ~/.bashrc && echo $PATH
  args:
    executable: /bin/bash

# Handle errors gracefully
- name: Check service status (may fail)
  ansible.builtin.shell: systemctl is-active myservice || true
  register: service_status
  changed_when: false

# Idempotent shell command
- name: Add line to config if not present
  ansible.builtin.shell: grep -q "myconfig" /etc/app.conf || echo "myconfig=value" >> /etc/app.conf
  args:
    creates: /etc/app.conf.configured
```

### ansible.builtin.file - Manage Files and Directories

Manages file and directory attributes including creation, deletion, permissions, ownership, and symbolic/hard links. This module is idempotent and handles the complete lifecycle of filesystem objects. Many other modules (copy, template) support the same file attribute options.

```yaml
# Create a directory with specific permissions
- name: Create application directory
  ansible.builtin.file:
    path: /opt/myapp
    state: directory
    owner: appuser
    group: appgroup
    mode: '0755'

# Create directory tree recursively
- name: Create nested directories
  ansible.builtin.file:
    path: /opt/myapp/data/cache/temp
    state: directory
    mode: '0755'
    recurse: yes

# Set permissions on existing file
- name: Secure configuration file
  ansible.builtin.file:
    path: /etc/myapp/config.yml
    owner: root
    group: myapp
    mode: '0640'

# Create a symbolic link
- name: Create symlink to current version
  ansible.builtin.file:
    src: /opt/myapp/releases/v1.2.3
    dest: /opt/myapp/current
    state: link
    owner: appuser
    group: appgroup

# Create a hard link
- name: Create hard link for backup
  ansible.builtin.file:
    src: /var/lib/myapp/data.db
    dest: /var/backups/data.db.link
    state: hard

# Remove a file
- name: Remove old configuration
  ansible.builtin.file:
    path: /etc/myapp/old_config.yml
    state: absent

# Remove directory recursively
- name: Clean up old release
  ansible.builtin.file:
    path: /opt/myapp/releases/v1.0.0
    state: absent

# Touch a file (create if missing, update timestamp)
- name: Create marker file
  ansible.builtin.file:
    path: /var/lib/myapp/.initialized
    state: touch
    mode: '0644'

# Set recursive ownership on directory
- name: Fix ownership on data directory
  ansible.builtin.file:
    path: /var/lib/myapp
    state: directory
    owner: appuser
    group: appgroup
    recurse: yes
```

### ansible.builtin.copy - Copy Files to Remote Hosts

Copies files from the control machine to remote hosts, or copies files between locations on remote hosts. Supports content generation, backup creation, and validation. For templating with variable substitution, use the `template` module instead.

```yaml
# Copy a file to remote host
- name: Copy configuration file
  ansible.builtin.copy:
    src: files/myapp.conf
    dest: /etc/myapp/myapp.conf
    owner: root
    group: myapp
    mode: '0644'
    backup: yes

# Copy with content (create file from string)
- name: Create configuration from content
  ansible.builtin.copy:
    content: |
      # Application Configuration
      database_host: localhost
      database_port: 5432
      log_level: info
    dest: /etc/myapp/config.yml
    owner: appuser
    group: appgroup
    mode: '0640'

# Copy directory recursively
- name: Copy entire config directory
  ansible.builtin.copy:
    src: files/config/
    dest: /etc/myapp/
    owner: root
    group: myapp
    directory_mode: '0755'

# Copy with validation (run command before replacing)
- name: Copy nginx configuration with validation
  ansible.builtin.copy:
    src: files/nginx.conf
    dest: /etc/nginx/nginx.conf
    owner: root
    group: root
    mode: '0644'
    validate: /usr/sbin/nginx -t -c %s
    backup: yes

# Remote to remote copy
- name: Copy file on remote host
  ansible.builtin.copy:
    src: /tmp/downloaded_file.tar.gz
    dest: /opt/packages/file.tar.gz
    remote_src: yes

# Copy with force disabled (don't overwrite if exists)
- name: Copy default config if not exists
  ansible.builtin.copy:
    src: files/default.conf
    dest: /etc/myapp/config.conf
    force: no
    owner: appuser
    mode: '0644'
```

### ansible.builtin.template - Render Jinja2 Templates

Processes Jinja2 templates and copies the rendered output to remote hosts. Templates can include variables, conditionals, loops, and filters. Essential for generating configuration files that vary by host or environment.

```yaml
# Basic template rendering
- name: Configure nginx from template
  ansible.builtin.template:
    src: templates/nginx.conf.j2
    dest: /etc/nginx/nginx.conf
    owner: root
    group: root
    mode: '0644'
    backup: yes
  notify: Reload nginx

# Template with validation
- name: Configure sshd
  ansible.builtin.template:
    src: templates/sshd_config.j2
    dest: /etc/ssh/sshd_config
    owner: root
    group: root
    mode: '0600'
    validate: /usr/sbin/sshd -t -f %s
  notify: Restart sshd

# Example template file (nginx.conf.j2):
# worker_processes {{ ansible_processor_vcpus }};
#
# events {
#     worker_connections {{ nginx_worker_connections | default(1024) }};
# }
#
# http {
#     server {
#         listen {{ nginx_port | default(80) }};
#         server_name {{ ansible_fqdn }};
#
#         {% for location in nginx_locations %}
#         location {{ location.path }} {
#             proxy_pass {{ location.backend }};
#         }
#         {% endfor %}
#     }
# }

# Template with custom delimiters (for files that use {{ }})
- name: Configure application with custom delimiters
  ansible.builtin.template:
    src: templates/app.conf.j2
    dest: /etc/myapp/app.conf
    variable_start_string: '[%'
    variable_end_string: '%]'

# Template with output encoding
- name: Create DOS-format config file
  ansible.builtin.template:
    src: templates/windows_config.j2
    dest: /share/config.ini
    newline_sequence: '\r\n'
```

### ansible.builtin.service - Manage System Services

Controls system services across various init systems including systemd, SysV init, OpenRC, Upstart, and others. Provides a unified interface for starting, stopping, restarting, and enabling services at boot. The module auto-detects the init system in use.

```yaml
# Start a service
- name: Start nginx
  ansible.builtin.service:
    name: nginx
    state: started

# Stop a service
- name: Stop nginx
  ansible.builtin.service:
    name: nginx
    state: stopped

# Restart a service (always)
- name: Restart nginx
  ansible.builtin.service:
    name: nginx
    state: restarted

# Reload service configuration (without restart)
- name: Reload nginx configuration
  ansible.builtin.service:
    name: nginx
    state: reloaded

# Enable service at boot
- name: Enable nginx to start on boot
  ansible.builtin.service:
    name: nginx
    enabled: yes

# Start and enable service
- name: Ensure nginx is running and enabled
  ansible.builtin.service:
    name: nginx
    state: started
    enabled: yes

# Check service by process pattern (when status is unreliable)
- name: Ensure legacy app is running
  ansible.builtin.service:
    name: legacy_app
    pattern: /usr/local/bin/legacy_app
    state: started

# Restart with sleep between stop and start
- name: Restart with delay for cleanup
  ansible.builtin.service:
    name: myapp
    state: restarted
    sleep: 5

# Handler example for conditional restarts
# In handlers/main.yml:
# - name: Reload nginx
#   ansible.builtin.service:
#     name: nginx
#     state: reloaded
```

### ansible.builtin.apt - Manage Debian/Ubuntu Packages

Manages APT packages on Debian-based systems. Supports package installation, removal, upgrades, and cache management. Handles version pinning, repository management, and dependency resolution automatically.

```yaml
# Install a single package
- name: Install nginx
  ansible.builtin.apt:
    name: nginx
    state: present

# Install multiple packages
- name: Install required packages
  ansible.builtin.apt:
    name:
      - nginx
      - postgresql
      - python3-pip
      - git
    state: present

# Install specific version
- name: Install specific nginx version
  ansible.builtin.apt:
    name: nginx=1.18.0-0ubuntu1
    state: present

# Update cache and install package
- name: Update cache and install nginx
  ansible.builtin.apt:
    name: nginx
    state: present
    update_cache: yes
    cache_valid_time: 3600

# Upgrade all packages
- name: Upgrade all packages
  ansible.builtin.apt:
    upgrade: dist
    update_cache: yes

# Remove a package
- name: Remove nginx
  ansible.builtin.apt:
    name: nginx
    state: absent

# Remove package and purge configuration
- name: Purge nginx completely
  ansible.builtin.apt:
    name: nginx
    state: absent
    purge: yes

# Install from .deb file
- name: Install local package
  ansible.builtin.apt:
    deb: /tmp/mypackage_1.0.0_amd64.deb

# Install from URL
- name: Install package from URL
  ansible.builtin.apt:
    deb: https://example.com/packages/mypackage_1.0.0_amd64.deb

# Clean up unnecessary packages
- name: Remove unused dependencies
  ansible.builtin.apt:
    autoremove: yes

# Install build dependencies
- name: Install build dependencies for nginx
  ansible.builtin.apt:
    name: nginx
    state: build-dep

# Full system update with cleanup
- name: Update and clean system
  ansible.builtin.apt:
    update_cache: yes
    upgrade: dist
    autoremove: yes
    autoclean: yes
```

### ansible.builtin.user - Manage User Accounts

Creates, modifies, and removes user accounts on Unix-like systems. Manages user attributes including UID, groups, home directory, shell, and password. Supports SSH key generation and various authentication settings.

```yaml
# Create a user
- name: Create application user
  ansible.builtin.user:
    name: appuser
    comment: "Application Service Account"
    uid: 1500
    group: appgroup
    shell: /bin/bash
    home: /home/appuser
    create_home: yes

# Create system user (no login shell, no home)
- name: Create nginx system user
  ansible.builtin.user:
    name: nginx
    system: yes
    shell: /sbin/nologin
    create_home: no

# Add user to supplementary groups
- name: Add user to docker group
  ansible.builtin.user:
    name: deploy
    groups: docker,sudo
    append: yes

# Set user password (hashed)
- name: Set user password
  ansible.builtin.user:
    name: admin
    password: "{{ 'plaintext_password' | password_hash('sha512') }}"
    update_password: always

# Create user with SSH key
- name: Create user with SSH key
  ansible.builtin.user:
    name: deploy
    generate_ssh_key: yes
    ssh_key_bits: 4096
    ssh_key_type: rsa
    ssh_key_comment: "deploy@{{ ansible_hostname }}"
    ssh_key_file: .ssh/id_rsa

# Remove user
- name: Remove old user
  ansible.builtin.user:
    name: olduser
    state: absent

# Remove user and their home directory
- name: Remove user completely
  ansible.builtin.user:
    name: olduser
    state: absent
    remove: yes
    force: yes

# Lock user account
- name: Lock user account
  ansible.builtin.user:
    name: suspended_user
    password_lock: yes

# Set account expiration
- name: Set user expiration date
  ansible.builtin.user:
    name: contractor
    expires: "{{ (ansible_date_time.epoch | int) + (86400 * 90) }}"

# Create user matching existing system
- name: Ensure consistent user across systems
  ansible.builtin.user:
    name: appuser
    uid: 1500
    group: appgroup
    groups:
      - developers
      - docker
    append: yes
    shell: /bin/bash
    home: /home/appuser
    create_home: yes
    state: present
```

### ansible.builtin.group - Manage Groups

Manages group accounts on Unix-like systems. Creates, modifies, and removes groups with specified GIDs. Groups should be created before users that reference them.

```yaml
# Create a group
- name: Create application group
  ansible.builtin.group:
    name: appgroup
    gid: 1500
    state: present

# Create system group
- name: Create nginx system group
  ansible.builtin.group:
    name: nginx
    system: yes
    state: present

# Remove a group
- name: Remove old group
  ansible.builtin.group:
    name: oldgroup
    state: absent

# Ensure multiple groups exist
- name: Create required groups
  ansible.builtin.group:
    name: "{{ item.name }}"
    gid: "{{ item.gid }}"
    state: present
  loop:
    - { name: developers, gid: 2000 }
    - { name: operators, gid: 2001 }
    - { name: readonly, gid: 2002 }
```

### ansible.builtin.get_url - Download Files from URLs

Downloads files from HTTP, HTTPS, or FTP URLs to remote hosts. Supports checksum verification, authentication, and conditional downloads. Handles redirects and can validate downloaded content.

```yaml
# Download a file
- name: Download application archive
  ansible.builtin.get_url:
    url: https://releases.example.com/myapp-1.2.3.tar.gz
    dest: /tmp/myapp-1.2.3.tar.gz
    mode: '0644'

# Download with checksum verification
- name: Download with SHA256 verification
  ansible.builtin.get_url:
    url: https://releases.example.com/myapp-1.2.3.tar.gz
    dest: /tmp/myapp-1.2.3.tar.gz
    checksum: sha256:a94a8fe5ccb19ba61c4c0873d391e987982fbbd3f3cc2e9a67a8c26c8f4b1a2e

# Download with checksum from URL
- name: Download with checksum file
  ansible.builtin.get_url:
    url: https://releases.example.com/myapp-1.2.3.tar.gz
    dest: /tmp/myapp-1.2.3.tar.gz
    checksum: sha256:https://releases.example.com/myapp-1.2.3.tar.gz.sha256

# Download with authentication
- name: Download from authenticated endpoint
  ansible.builtin.get_url:
    url: https://packages.example.com/private/myapp.tar.gz
    dest: /tmp/myapp.tar.gz
    url_username: "{{ download_user }}"
    url_password: "{{ download_password }}"
    force_basic_auth: yes

# Download with custom headers
- name: Download with API token
  ansible.builtin.get_url:
    url: https://api.github.com/repos/owner/repo/releases/latest
    dest: /tmp/release_info.json
    headers:
      Authorization: "Bearer {{ github_token }}"
      Accept: application/vnd.github.v3+json

# Conditional download (only if changed)
- name: Download only if remote file is newer
  ansible.builtin.get_url:
    url: https://releases.example.com/myapp-latest.tar.gz
    dest: /tmp/myapp-latest.tar.gz
    force: no

# Download with timeout and retries
- name: Download large file with retries
  ansible.builtin.get_url:
    url: https://releases.example.com/large-file.iso
    dest: /tmp/large-file.iso
    timeout: 300
  retries: 3
  delay: 10
```

### ansible.builtin.unarchive - Extract Archives

Extracts archive files (tar, zip, etc.) on remote hosts. Can copy archives from the control machine and extract them, or extract archives already on the remote host. Supports various archive formats and extraction options.

```yaml
# Copy and extract archive
- name: Extract application archive
  ansible.builtin.unarchive:
    src: files/myapp-1.2.3.tar.gz
    dest: /opt/myapp/
    owner: appuser
    group: appgroup

# Extract archive already on remote host
- name: Extract downloaded archive
  ansible.builtin.unarchive:
    src: /tmp/myapp-1.2.3.tar.gz
    dest: /opt/myapp/
    remote_src: yes

# Extract with options
- name: Extract with specific options
  ansible.builtin.unarchive:
    src: /tmp/myapp.tar.gz
    dest: /opt/myapp/
    remote_src: yes
    extra_opts:
      - --strip-components=1
    owner: appuser
    group: appgroup
    mode: '0755'

# Extract only if target doesn't exist (idempotent)
- name: Extract if not already done
  ansible.builtin.unarchive:
    src: /tmp/myapp.tar.gz
    dest: /opt/myapp/
    remote_src: yes
    creates: /opt/myapp/bin/myapp

# Download and extract in one step
- name: Download and extract
  ansible.builtin.unarchive:
    src: https://releases.example.com/myapp-1.2.3.tar.gz
    dest: /opt/myapp/
    remote_src: yes

# Extract specific files from archive
- name: Extract only config files
  ansible.builtin.unarchive:
    src: /tmp/myapp.tar.gz
    dest: /etc/myapp/
    remote_src: yes
    include:
      - "config/*"
      - "*.yml"
```

### ansible.builtin.lineinfile - Manage Lines in Files

Ensures a particular line is present or absent in a file. Useful for simple configuration changes, toggling settings, and managing single lines. For complex multi-line changes or full file management, consider `template` or `blockinfile`.

```yaml
# Ensure a line is present
- name: Ensure JAVA_HOME is set in profile
  ansible.builtin.lineinfile:
    path: /etc/profile.d/java.sh
    line: 'export JAVA_HOME=/usr/lib/jvm/java-11'
    create: yes
    mode: '0644'

# Replace a line matching pattern
- name: Set max open files limit
  ansible.builtin.lineinfile:
    path: /etc/security/limits.conf
    regexp: '^\* soft nofile'
    line: '* soft nofile 65535'

# Add line after a specific pattern
- name: Add setting after section header
  ansible.builtin.lineinfile:
    path: /etc/myapp.conf
    insertafter: '^\[database\]'
    line: 'max_connections = 100'

# Add line before a specific pattern
- name: Add comment before setting
  ansible.builtin.lineinfile:
    path: /etc/myapp.conf
    insertbefore: '^max_connections'
    line: '# Maximum database connections'

# Remove a line
- name: Remove deprecated setting
  ansible.builtin.lineinfile:
    path: /etc/myapp.conf
    regexp: '^legacy_mode.*'
    state: absent

# Ensure line with backup
- name: Update configuration with backup
  ansible.builtin.lineinfile:
    path: /etc/myapp.conf
    regexp: '^listen_port='
    line: 'listen_port=8080'
    backup: yes

# Multiple replacements with validation
- name: Configure sshd settings
  ansible.builtin.lineinfile:
    path: /etc/ssh/sshd_config
    regexp: "{{ item.regexp }}"
    line: "{{ item.line }}"
    validate: /usr/sbin/sshd -t -f %s
  loop:
    - { regexp: '^#?PermitRootLogin', line: 'PermitRootLogin no' }
    - { regexp: '^#?PasswordAuthentication', line: 'PasswordAuthentication no' }
    - { regexp: '^#?MaxAuthTries', line: 'MaxAuthTries 3' }
  notify: Restart sshd
```

### ansible.builtin.blockinfile - Manage Blocks of Text

Inserts, updates, or removes blocks of multi-line text in files. Blocks are surrounded by marker lines for identification and management. Ideal for adding configuration sections that should be managed as a unit.

```yaml
# Add a configuration block
- name: Add custom SSH banner
  ansible.builtin.blockinfile:
    path: /etc/ssh/sshd_banner
    create: yes
    mode: '0644'
    block: |
      ****************************************************
      *  Authorized access only. All activity logged.    *
      ****************************************************

# Add block with custom markers
- name: Add nginx server block
  ansible.builtin.blockinfile:
    path: /etc/nginx/conf.d/myapp.conf
    create: yes
    marker: "# {mark} ANSIBLE MANAGED - myapp upstream"
    block: |
      upstream myapp {
          server 127.0.0.1:8001;
          server 127.0.0.1:8002;
          server 127.0.0.1:8003;
      }

# Insert block after a pattern
- name: Add hosts entries
  ansible.builtin.blockinfile:
    path: /etc/hosts
    insertafter: '^127\.0\.0\.1'
    marker: "# {mark} ANSIBLE MANAGED - internal hosts"
    block: |
      192.168.1.10  app-server-1.internal
      192.168.1.11  app-server-2.internal
      192.168.1.20  db-server.internal

# Remove a managed block
- name: Remove old configuration block
  ansible.builtin.blockinfile:
    path: /etc/myapp.conf
    marker: "# {mark} OLD CONFIG"
    state: absent

# Add block with backup
- name: Add iptables rules
  ansible.builtin.blockinfile:
    path: /etc/iptables/rules.v4
    backup: yes
    marker: "# {mark} ANSIBLE MANAGED - app rules"
    block: |
      -A INPUT -p tcp --dport 80 -j ACCEPT
      -A INPUT -p tcp --dport 443 -j ACCEPT
      -A INPUT -p tcp --dport 22 -j ACCEPT
```

### ansible.builtin.cron - Manage Cron Jobs

Manages cron jobs for users on Unix-like systems. Can create, modify, and remove cron entries including scheduled commands, environment variables, and special time specifications.

```yaml
# Create a cron job
- name: Run backup script daily
  ansible.builtin.cron:
    name: "daily database backup"
    minute: "0"
    hour: "2"
    job: "/opt/scripts/backup-db.sh >> /var/log/backup.log 2>&1"
    user: postgres

# Create cron job with special time
- name: Run cleanup weekly
  ansible.builtin.cron:
    name: "weekly cleanup"
    special_time: weekly
    job: "/opt/scripts/cleanup.sh"

# Create cron job that runs every 5 minutes
- name: Health check every 5 minutes
  ansible.builtin.cron:
    name: "health check"
    minute: "*/5"
    job: "/opt/scripts/health-check.sh"

# Create cron environment variable
- name: Set PATH for cron
  ansible.builtin.cron:
    name: PATH
    env: yes
    job: /usr/local/bin:/usr/bin:/bin
    user: appuser

# Create cron job with environment
- name: Run report with custom environment
  ansible.builtin.cron:
    name: "daily report"
    minute: "30"
    hour: "6"
    job: "/opt/scripts/report.sh"
    user: reporter
  environment:
    MAILTO: admin@example.com
    REPORT_FORMAT: html

# Remove a cron job
- name: Remove old cron job
  ansible.builtin.cron:
    name: "old backup job"
    state: absent
    user: postgres

# Disable a cron job (comment out)
- name: Temporarily disable maintenance job
  ansible.builtin.cron:
    name: "weekly maintenance"
    minute: "0"
    hour: "3"
    weekday: "0"
    job: "/opt/scripts/maintenance.sh"
    disabled: yes
```

### ansible.builtin.debug - Print Debug Messages

Prints statements during playbook execution for debugging purposes. Useful for displaying variable values, execution flow, and troubleshooting. Messages are shown only when tasks are executed and can be controlled with verbosity levels.

```yaml
# Print a simple message
- name: Display progress
  ansible.builtin.debug:
    msg: "Starting application deployment"

# Display a variable
- name: Show gathered facts
  ansible.builtin.debug:
    var: ansible_distribution

# Display multiple variables
- name: Show deployment info
  ansible.builtin.debug:
    msg: |
      Deploying to: {{ inventory_hostname }}
      OS: {{ ansible_distribution }} {{ ansible_distribution_version }}
      IP: {{ ansible_default_ipv4.address }}
      Memory: {{ ansible_memtotal_mb }} MB

# Display only at specific verbosity
- name: Detailed debug info (only with -v)
  ansible.builtin.debug:
    msg: "Detailed variable dump: {{ hostvars[inventory_hostname] }}"
    verbosity: 1

# Display registered variable
- name: Run command and show output
  ansible.builtin.command: uptime
  register: uptime_result

- name: Display uptime
  ansible.builtin.debug:
    var: uptime_result.stdout

# Conditional debug
- name: Debug when condition met
  ansible.builtin.debug:
    msg: "Running in production mode"
  when: environment == "production"
```

### ansible.builtin.assert - Verify Conditions

Verifies that given expressions are true, failing the playbook if they are not. Used to validate prerequisites, check configuration values, and ensure system state before proceeding. Essential for defensive playbook design.

```yaml
# Assert a condition is true
- name: Verify minimum memory
  ansible.builtin.assert:
    that:
      - ansible_memtotal_mb >= 2048
    fail_msg: "Server must have at least 2GB RAM"
    success_msg: "Memory check passed: {{ ansible_memtotal_mb }}MB available"

# Multiple assertions
- name: Verify deployment prerequisites
  ansible.builtin.assert:
    that:
      - ansible_distribution == "Ubuntu"
      - ansible_distribution_major_version | int >= 20
      - ansible_python_version is version('3.8', '>=')
    fail_msg: "This playbook requires Ubuntu 20+ with Python 3.8+"

# Assert variable is defined
- name: Verify required variables
  ansible.builtin.assert:
    that:
      - deploy_version is defined
      - deploy_version | length > 0
      - api_key is defined
    fail_msg: "Required variables deploy_version and api_key must be set"

# Assert file exists (after gathering)
- name: Check configuration file exists
  ansible.builtin.stat:
    path: /etc/myapp/config.yml
  register: config_file

- name: Assert configuration exists
  ansible.builtin.assert:
    that:
      - config_file.stat.exists
      - config_file.stat.isreg
    fail_msg: "Configuration file /etc/myapp/config.yml must exist"

# Assert service is running
- name: Check database is accessible
  ansible.builtin.command: pg_isready -h localhost
  register: pg_check
  changed_when: false
  failed_when: false

- name: Assert database is running
  ansible.builtin.assert:
    that:
      - pg_check.rc == 0
    fail_msg: "PostgreSQL database must be running before deployment"
    quiet: yes
```

### ansible.builtin.stat - Get File Status

Retrieves status information about files and directories on remote hosts. Returns facts including existence, type, permissions, ownership, timestamps, and checksums. Essential for conditional task execution based on filesystem state.

```yaml
# Check if file exists
- name: Check configuration file
  ansible.builtin.stat:
    path: /etc/myapp/config.yml
  register: config_stat

- name: Create default config if missing
  ansible.builtin.copy:
    src: files/default_config.yml
    dest: /etc/myapp/config.yml
  when: not config_stat.stat.exists

# Check file checksum
- name: Get current binary checksum
  ansible.builtin.stat:
    path: /opt/myapp/bin/myapp
    checksum_algorithm: sha256
  register: current_binary

- name: Update binary if changed
  ansible.builtin.copy:
    src: files/myapp
    dest: /opt/myapp/bin/myapp
  when: current_binary.stat.checksum != expected_checksum

# Check if path is a directory
- name: Verify data directory
  ansible.builtin.stat:
    path: /var/lib/myapp/data
  register: data_dir

- name: Create data directory
  ansible.builtin.file:
    path: /var/lib/myapp/data
    state: directory
  when: not data_dir.stat.exists or not data_dir.stat.isdir

# Check file permissions
- name: Verify secure permissions
  ansible.builtin.stat:
    path: /etc/myapp/secrets.yml
  register: secrets_stat

- name: Fail if permissions too open
  ansible.builtin.fail:
    msg: "Secrets file has insecure permissions"
  when:
    - secrets_stat.stat.exists
    - secrets_stat.stat.mode != '0600'

# Check symbolic link
- name: Check current version link
  ansible.builtin.stat:
    path: /opt/myapp/current
  register: current_link

- name: Display current version
  ansible.builtin.debug:
    msg: "Current version: {{ current_link.stat.lnk_source | basename }}"
  when: current_link.stat.islnk
```

### ansible.builtin.wait_for - Wait for Conditions

Waits for a condition to be satisfied before continuing. Can wait for ports to be available, files to exist, processes to stop, or search patterns in files. Essential for orchestrating dependencies and ensuring services are ready.

```yaml
# Wait for port to be available
- name: Wait for web server to start
  ansible.builtin.wait_for:
    port: 80
    delay: 5
    timeout: 60

# Wait for remote port
- name: Wait for database to be ready
  ansible.builtin.wait_for:
    host: db.example.com
    port: 5432
    delay: 10
    timeout: 300

# Wait for file to exist
- name: Wait for application to create PID file
  ansible.builtin.wait_for:
    path: /var/run/myapp.pid
    state: present
    timeout: 30

# Wait for file to contain pattern
- name: Wait for application to be ready
  ansible.builtin.wait_for:
    path: /var/log/myapp/startup.log
    search_regex: "Application started successfully"
    timeout: 120

# Wait for file to be removed
- name: Wait for lock file to be released
  ansible.builtin.wait_for:
    path: /var/lock/myapp.lock
    state: absent
    timeout: 60

# Wait for port to close
- name: Wait for old process to stop
  ansible.builtin.wait_for:
    port: 8080
    state: stopped
    timeout: 30

# Wait for connection to database
- name: Wait for PostgreSQL
  ansible.builtin.wait_for:
    host: "{{ db_host }}"
    port: 5432
    state: started
    delay: 5
    connect_timeout: 5
    timeout: 300
  register: db_ready
  retries: 3

# Combination wait in handlers
# handlers/main.yml:
- name: Wait for application restart
  ansible.builtin.wait_for:
    port: 8080
    delay: 5
    timeout: 60
  listen: "restart application"
```

### ansible.builtin.uri - Interact with HTTP Services

Interacts with HTTP and HTTPS web services. Performs requests to APIs, downloads content, and validates web endpoints. Supports all HTTP methods, authentication, headers, and body content for comprehensive API automation.

```yaml
# Simple GET request
- name: Check service health
  ansible.builtin.uri:
    url: http://localhost:8080/health
    return_content: yes
  register: health_check

- name: Verify healthy status
  ansible.builtin.assert:
    that:
      - health_check.status == 200
      - "'healthy' in health_check.content"

# POST request with JSON body
- name: Create user via API
  ansible.builtin.uri:
    url: https://api.example.com/users
    method: POST
    body_format: json
    body:
      username: "{{ new_user }}"
      email: "{{ user_email }}"
      role: admin
    headers:
      Authorization: "Bearer {{ api_token }}"
    status_code: [200, 201]
  register: create_result

# PUT request to update resource
- name: Update configuration via API
  ansible.builtin.uri:
    url: "https://api.example.com/config/{{ config_id }}"
    method: PUT
    body_format: json
    body: "{{ config_data }}"
    headers:
      Authorization: "Bearer {{ api_token }}"
      Content-Type: application/json

# DELETE request
- name: Remove resource
  ansible.builtin.uri:
    url: "https://api.example.com/resources/{{ resource_id }}"
    method: DELETE
    headers:
      Authorization: "Bearer {{ api_token }}"
    status_code: [200, 204, 404]

# API request with retry
- name: Wait for service to be ready
  ansible.builtin.uri:
    url: http://localhost:8080/ready
    method: GET
  register: result
  until: result.status == 200
  retries: 30
  delay: 10

# Download file from authenticated endpoint
- name: Download report
  ansible.builtin.uri:
    url: https://api.example.com/reports/latest
    method: GET
    dest: /tmp/report.pdf
    url_username: "{{ api_user }}"
    url_password: "{{ api_pass }}"
    force_basic_auth: yes

# Validate SSL certificate
- name: Check SSL certificate
  ansible.builtin.uri:
    url: https://example.com
    method: GET
    validate_certs: yes
  register: ssl_check
```

## Playbook Structure and Patterns

### Complete Playbook Example

```yaml
---
# site.yml - Main playbook demonstrating common patterns
- name: Deploy Web Application
  hosts: webservers
  become: yes
  gather_facts: yes

  vars:
    app_name: myapp
    app_version: "1.2.3"
    app_user: appuser
    app_group: appgroup
    app_port: 8080

  vars_files:
    - vars/common.yml
    - "vars/{{ environment }}.yml"

  pre_tasks:
    - name: Update apt cache
      ansible.builtin.apt:
        update_cache: yes
        cache_valid_time: 3600
      when: ansible_os_family == "Debian"

    - name: Verify disk space
      ansible.builtin.assert:
        that:
          - ansible_mounts | selectattr('mount', 'equalto', '/') | map(attribute='size_available') | first > 1073741824
        fail_msg: "Insufficient disk space on root partition"

  roles:
    - role: common
      tags: [common, always]
    - role: nginx
      tags: [webserver, nginx]
    - role: application
      tags: [application]

  tasks:
    - name: Create application directories
      ansible.builtin.file:
        path: "{{ item }}"
        state: directory
        owner: "{{ app_user }}"
        group: "{{ app_group }}"
        mode: '0755'
      loop:
        - "/opt/{{ app_name }}"
        - "/opt/{{ app_name }}/releases"
        - "/opt/{{ app_name }}/shared"
        - "/var/log/{{ app_name }}"

    - name: Download application
      ansible.builtin.get_url:
        url: "https://releases.example.com/{{ app_name }}-{{ app_version }}.tar.gz"
        dest: "/tmp/{{ app_name }}-{{ app_version }}.tar.gz"
        checksum: "sha256:{{ app_checksum }}"
      register: download_result

    - name: Extract application
      ansible.builtin.unarchive:
        src: "/tmp/{{ app_name }}-{{ app_version }}.tar.gz"
        dest: "/opt/{{ app_name }}/releases/"
        remote_src: yes
        owner: "{{ app_user }}"
        group: "{{ app_group }}"
      when: download_result.changed

    - name: Deploy configuration
      ansible.builtin.template:
        src: templates/config.yml.j2
        dest: "/opt/{{ app_name }}/shared/config.yml"
        owner: "{{ app_user }}"
        group: "{{ app_group }}"
        mode: '0640'
      notify: Restart application

    - name: Update current symlink
      ansible.builtin.file:
        src: "/opt/{{ app_name }}/releases/{{ app_version }}"
        dest: "/opt/{{ app_name }}/current"
        state: link
        owner: "{{ app_user }}"
        group: "{{ app_group }}"
      notify: Restart application

    - name: Install systemd service
      ansible.builtin.template:
        src: templates/systemd.service.j2
        dest: "/etc/systemd/system/{{ app_name }}.service"
        mode: '0644'
      notify:
        - Reload systemd
        - Restart application

    - name: Ensure service is running
      ansible.builtin.service:
        name: "{{ app_name }}"
        state: started
        enabled: yes

  post_tasks:
    - name: Wait for application to be ready
      ansible.builtin.uri:
        url: "http://localhost:{{ app_port }}/health"
        status_code: 200
      register: result
      until: result.status == 200
      retries: 30
      delay: 5

    - name: Verify deployment
      ansible.builtin.debug:
        msg: "Successfully deployed {{ app_name }} version {{ app_version }}"

  handlers:
    - name: Reload systemd
      ansible.builtin.systemd:
        daemon_reload: yes

    - name: Restart application
      ansible.builtin.service:
        name: "{{ app_name }}"
        state: restarted
```

### Inventory Example

```ini
# inventory/production
[webservers]
web1.example.com ansible_host=192.168.1.10
web2.example.com ansible_host=192.168.1.11
web3.example.com ansible_host=192.168.1.12

[dbservers]
db1.example.com ansible_host=192.168.1.20
db2.example.com ansible_host=192.168.1.21

[loadbalancers]
lb1.example.com ansible_host=192.168.1.5

[production:children]
webservers
dbservers
loadbalancers

[production:vars]
environment=production
ansible_user=deploy
ansible_ssh_private_key_file=~/.ssh/production_key

[webservers:vars]
nginx_worker_processes=auto
app_instances=4

[dbservers:vars]
postgresql_max_connections=200
```

```yaml
# inventory/production.yml (YAML format)
all:
  children:
    production:
      children:
        webservers:
          hosts:
            web1.example.com:
              ansible_host: 192.168.1.10
              app_instances: 4
            web2.example.com:
              ansible_host: 192.168.1.11
              app_instances: 4
        dbservers:
          hosts:
            db1.example.com:
              ansible_host: 192.168.1.20
              postgresql_role: primary
            db2.example.com:
              ansible_host: 192.168.1.21
              postgresql_role: replica
      vars:
        environment: production
        ansible_user: deploy
```

## Summary

Ansible Core provides a comprehensive, agentless IT automation framework that enables infrastructure as code through human-readable YAML playbooks. The platform excels at configuration management across heterogeneous environments, supporting multiple operating systems (Linux distributions, BSD variants, macOS, Windows), init systems (systemd, SysV, Upstart, OpenRC), and package managers (apt, yum, dnf, zypper) through a unified module interface. The push-based architecture eliminates the need for managed agents, using standard SSH connections and Python interpreters already present on most systems.

The modular design allows seamless integration with existing infrastructure through the plugin system, supporting custom inventory sources (static files, dynamic scripts, cloud providers), connection methods (SSH, WinRM, local, Docker), callback plugins for output customization, and filter plugins for data transformation. Organizations typically structure their automation using roles for reusable components, collections for distributing related content, and group_vars/host_vars for environment-specific configuration, enabling consistent deployments across development, staging, and production environments while maintaining a single source of truth in version-controlled playbook repositories.
