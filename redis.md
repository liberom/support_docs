# Redis Documentation

Redis is an open-source, in-memory data structure store used as a database, cache, message broker, and streaming engine. This documentation repository powers redis.io/docs and provides comprehensive guidance for Redis's core data types (strings, hashes, lists, sets, sorted sets, streams), extended modules (JSON, Search, TimeSeries, Vector Sets, Probabilistic structures), client libraries across 8+ programming languages, and operational deployment options including Redis Cloud, Redis Software, and Kubernetes.

The documentation covers over 537 Redis commands with detailed syntax, complexity analysis, and working examples. It includes integration guides for AI/ML frameworks like LangChain and RedisVL, data synchronization tools, and production deployment patterns. Client libraries are documented for Python (redis-py), Go (go-redis), Java (Jedis, Lettuce), Node.js (node-redis), .NET (NRedisStack), PHP, Rust, and C (hiredis), with connection examples, TLS configuration, clustering support, and client-side caching.

## Core String Commands

### SET - Store a String Value

Sets the string value of a key. If the key already holds a value, it is overwritten. Supports conditional options (NX/XX), expiration (EX/PX/EXAT/PXAT), and atomic get-and-set (GET option).

```bash
# Basic SET and GET
SET mykey "Hello"
GET mykey
# Returns: "Hello"

# SET with expiration (60 seconds)
SET anotherkey "will expire in a minute" EX 60

# SET only if key does not exist (NX)
SET resource-name "lock-value" NX EX 30

# SET only if key exists (XX) and return old value (GET)
SET mykey "NewValue" XX GET
# Returns: "Hello" (old value)

# Using redis-py (Python)
import redis
r = redis.Redis(host='localhost', port=6379, decode_responses=True)
r.set('foo', 'bar')
r.set('session', 'data', ex=3600)  # Expires in 1 hour
value = r.get('foo')  # Returns: 'bar'
```

## Hash Commands

### HSET - Set Hash Fields

Creates or modifies the value of fields in a hash. Returns the number of new fields added. Useful for storing objects with multiple attributes.

```bash
# Set single field
HSET myhash field1 "Hello"
# Returns: (integer) 1

# Set multiple fields at once
HSET myhash field2 "Hi" field3 "World"
# Returns: (integer) 2

# Get all fields and values
HGETALL myhash
# Returns:
# 1) "field1"
# 2) "Hello"
# 3) "field2"
# 4) "Hi"
# 5) "field3"
# 6) "World"

# Using redis-py (Python)
r.hset('user-session:123', mapping={
    'name': 'John',
    'surname': 'Smith',
    'company': 'Redis',
    'age': 29
})
user = r.hgetall('user-session:123')
# Returns: {'name': 'John', 'surname': 'Smith', 'company': 'Redis', 'age': '29'}
```

## List Commands

### LPUSH - Add Elements to List Head

Inserts elements at the head of a list. Creates the list if it doesn't exist. Elements are inserted left-to-right, so the rightmost element ends up at the head.

```bash
# Add single element
LPUSH mylist "world"
# Returns: (integer) 1

# Add another element (becomes first)
LPUSH mylist "hello"
# Returns: (integer) 2

# Get all elements
LRANGE mylist 0 -1
# Returns:
# 1) "hello"
# 2) "world"

# Add multiple elements at once
LPUSH mylist "a" "b" "c"
# Returns: (integer) 5
# List now: ["c", "b", "a", "hello", "world"]

# Using Node.js
await client.lPush('mylist', 'world');
await client.lPush('mylist', 'hello');
const list = await client.lRange('mylist', 0, -1);
// Returns: ['hello', 'world']
```

## Sorted Set Commands

### ZADD - Add Members with Scores

Adds members to a sorted set with scores. Members are ordered by score (ascending). Supports conditional updates (NX/XX/GT/LT) and increment mode (INCR).

```bash
# Add single member
ZADD myzset 1 "one"
# Returns: (integer) 1

# Add multiple members
ZADD myzset 2 "two" 3 "three"
# Returns: (integer) 2

# Get members with scores (sorted by score)
ZRANGE myzset 0 -1 WITHSCORES
# Returns:
# 1) "one"
# 2) "1"
# 3) "two"
# 4) "2"
# 5) "three"
# 6) "3"

# Update only if new score is greater (GT)
ZADD myzset GT 5 "one"
# Returns: (integer) 0 (no new members, but score updated)

# Increment score (like ZINCRBY)
ZADD myzset INCR 10 "two"
# Returns: "12" (new score)

# Using Go
ctx := context.Background()
client.ZAdd(ctx, "leaderboard", redis.Z{Score: 100, Member: "player1"})
client.ZAdd(ctx, "leaderboard", redis.Z{Score: 200, Member: "player2"})
result, _ := client.ZRangeWithScores(ctx, "leaderboard", 0, -1).Result()
```

## Stream Commands

### XADD - Append to Stream

Appends a new entry to a stream. Auto-generates entry IDs with `*`. Supports trimming (MAXLEN/MINID) to cap stream size.

```bash
# Add entry with auto-generated ID
XADD mystream * name Sara surname OConnor
# Returns: "1526919030474-0" (auto-generated ID)

# Add entry with multiple fields
XADD mystream * field1 value1 field2 value2 field3 value3
# Returns: "1526919030475-0"

# Check stream length
XLEN mystream
# Returns: (integer) 2

# Read all entries
XRANGE mystream - +
# Returns all entries with their IDs and field-value pairs

# Add with MAXLEN trimming (keep ~1000 entries)
XADD mystream MAXLEN ~ 1000 * sensor_id 1234 temperature 19.8

# Using redis-py
r.xadd('events', {'action': 'login', 'user': 'alice'})
r.xadd('events', {'action': 'purchase', 'item': 'book'}, maxlen=10000)
entries = r.xrange('events', '-', '+')
```

## JSON Commands

### JSON.SET and JSON.GET - Store and Retrieve JSON

Stores and retrieves JSON documents. Supports JSONPath syntax for accessing nested elements. Requires the RedisJSON module.

```bash
# Set a simple JSON string
JSON.SET bike $ '"Hyperion"'
# Returns: OK

# Get JSON value
JSON.GET bike $
# Returns: "[\"Hyperion\"]"

# Set a JSON object
JSON.SET bike:1 $ '{"model": "Deimos", "brand": "Ergonom", "price": 4972}'
# Returns: OK

# Get specific field using JSONPath
JSON.GET bike:1 $.model
# Returns: "[\"Deimos\"]"

# Modify nested value
JSON.SET bike:1 $.price 4500

# Numeric operations
JSON.SET crashes $ 0
JSON.NUMINCRBY crashes $ 1
# Returns: "[1]"
JSON.NUMMULTBY crashes $ 24
# Returns: "[24]"

# Array operations
JSON.SET riders $ '[]'
JSON.ARRAPPEND riders $ '"Norem"'
JSON.ARRINSERT riders $ 1 '"Prickett"' '"Royce"'
JSON.GET riders $
# Returns: "[[\"Norem\",\"Prickett\",\"Royce\"]]"

# Object inspection
JSON.OBJLEN bike:1 $
# Returns: (integer) 3
JSON.OBJKEYS bike:1 $
# Returns: ["model", "brand", "price"]
```

## Search Commands

### FT.CREATE - Create Search Index

Creates a full-text search index on Hash or JSON documents. Supports TEXT, TAG, NUMERIC, GEO, VECTOR, and GEOSHAPE field types.

```bash
# Create index on Hash documents
FT.CREATE idx ON HASH PREFIX 1 blog:post: SCHEMA
  title TEXT SORTABLE
  published_at NUMERIC SORTABLE
  category TAG SORTABLE

# Create index on JSON documents
FT.CREATE idx ON JSON SCHEMA
  $.title AS title TEXT
  $.categories AS categories TAG

# Create index with multiple prefixes
FT.CREATE author-books-idx ON HASH PREFIX 2 author:details: book:details: SCHEMA
  author_id TAG SORTABLE
  author_ids TAG
  title TEXT
  name TEXT

# Create vector search index
FT.CREATE books-idx ON HASH PREFIX 1 book: SCHEMA
  title TEXT
  title_embedding VECTOR HNSW 6 TYPE FLOAT32 DIM 384 DISTANCE_METRIC COSINE
```

### FT.SEARCH - Search the Index

Searches the index with text queries, filters, and vector similarity. Returns matching documents with their fields.

```bash
# Full-text search
FT.SEARCH books-idx "wizard"

# Search specific field
FT.SEARCH books-idx "@title:dogs"

# Numeric range search
FT.SEARCH books-idx "@published_at:[2020 2021]"

# Geo search (within 5km radius)
FT.SEARCH restaurants-idx "chinese @location:[-122.41 37.77 5 km]"

# Tag search
FT.SEARCH books-idx "@title:space @categories:{science}"

# Pagination and field selection
FT.SEARCH books-idx "python" LIMIT 10 10 RETURN 1 title

# Vector similarity search (KNN)
FT.SEARCH books-idx "*=>[KNN 10 @title_embedding $query_vec AS title_score]"
  PARAMS 2 query_vec <embedding_blob>
  SORTBY title_score
  DIALECT 2

# Using redis-py
from redis.commands.search.query import Query
q = Query("wizard").paging(0, 10).return_fields("title", "author")
results = r.ft("books-idx").search(q)
```

## Python Client (redis-py)

### Connection and Basic Operations

Connects to Redis server with support for connection pooling, TLS, clustering, and client-side caching.

```python
import redis
from redis.cluster import RedisCluster
from redis.cache import CacheConfig

# Basic connection
r = redis.Redis(host='localhost', port=6379, decode_responses=True)

# Connection with URL
r = redis.Redis.from_url("redis://localhost:6379/0")

# Connection with TLS
r = redis.Redis(
    host="my-redis.cloud.redislabs.com",
    port=6379,
    username="default",
    password="secret",
    ssl=True,
    ssl_certfile="./redis_user.crt",
    ssl_keyfile="./redis_user_private.key",
    ssl_ca_certs="./redis_ca.pem",
)

# Cluster connection
rc = RedisCluster(host='localhost', port=16379)
rc.set('foo', 'bar')
rc.get('foo')

# Connection pool
pool = redis.ConnectionPool().from_url("redis://localhost")
r1 = redis.Redis().from_pool(pool)
r2 = redis.Redis().from_pool(pool)
r1.set("key1", "value1")
r2.set("key2", "value2")
r1.close()
r2.close()
pool.close()

# Client-side caching (requires RESP3)
r = redis.Redis(
    protocol=3,
    cache_config=CacheConfig(),
    decode_responses=True
)
r.set("city", "New York")
r.get("city")  # Retrieved from server, cached
r.get("city")  # Retrieved from cache
```

## Go Client (go-redis)

### Connection and Operations

Full-featured Go client with context support, connection pooling, and cluster support.

```go
import (
    "context"
    "github.com/redis/go-redis/v9"
)

// Basic connection
client := redis.NewClient(&redis.Options{
    Addr:     "localhost:6379",
    Password: "",
    DB:       0,
    Protocol: 2,
})

// Connection from URL
opt, _ := redis.ParseURL("redis://user:pass@localhost:6379/0")
client := redis.NewClient(opt)

// Cluster connection
cluster := redis.NewClusterClient(&redis.ClusterOptions{
    Addrs: []string{":16379", ":16380", ":16381"},
    // RouteByLatency: true,
})

// Basic operations
ctx := context.Background()

// String operations
err := client.Set(ctx, "foo", "bar", 0).Err()
val, err := client.Get(ctx, "foo").Result()

// Hash operations
client.HSet(ctx, "user:1", "name", "John", "age", "30")
user, _ := client.HGetAll(ctx, "user:1").Result()

// List operations
client.LPush(ctx, "queue", "task1", "task2")
task, _ := client.RPop(ctx, "queue").Result()

// Sorted set operations
client.ZAdd(ctx, "leaderboard", redis.Z{Score: 100, Member: "player1"})
leaders, _ := client.ZRevRangeWithScores(ctx, "leaderboard", 0, 9).Result()

// Pipeline for batch operations
pipe := client.Pipeline()
pipe.Set(ctx, "key1", "value1", 0)
pipe.Set(ctx, "key2", "value2", 0)
pipe.Incr(ctx, "counter")
_, err = pipe.Exec(ctx)
```

## Node.js Client (node-redis)

### Connection and Async Operations

Modern async/await client with TypeScript support, clustering, and client-side caching.

```javascript
import { createClient, createCluster } from 'redis';

// Basic connection
const client = createClient();
client.on('error', err => console.log('Redis Client Error', err));
await client.connect();

// Connection with URL
const client = createClient({
    url: 'redis://alice:foobared@awesome.redis.server:6380'
});

// TLS connection
const client = createClient({
    username: 'default',
    password: 'secret',
    socket: {
        host: 'my-redis.cloud.redislabs.com',
        port: 6379,
        tls: true,
        key: readFileSync('./redis_user_private.key'),
        cert: readFileSync('./redis_user.crt'),
        ca: [readFileSync('./redis_ca.pem')]
    }
});

// Cluster connection
const cluster = createCluster({
    rootNodes: [
        { url: 'redis://127.0.0.1:16379' },
        { url: 'redis://127.0.0.1:16380' }
    ]
});
await cluster.connect();

// Basic operations
await client.set('key', 'value');
const value = await client.get('key');

// Hash operations
await client.hSet('user-session:123', {
    name: 'John',
    surname: 'Smith',
    company: 'Redis',
    age: 29
});
const userSession = await client.hGetAll('user-session:123');

// Client-side caching
const client = createClient({
    RESP: 3,
    clientSideCache: {
        ttl: 0,
        maxEntries: 0,
        evictPolicy: "LRU"
    }
});

// Cleanup
await client.quit();
```

## Time Series Commands

### TS.CREATE and TS.ADD - Create and Add Data Points

Creates time series keys and adds timestamped data points. Supports labels, retention policies, and compaction rules.

```bash
# Create time series
TS.CREATE thermometer:1

# Create with retention and labels
TS.CREATE thermometer:2 RETENTION 86400000 LABELS location UK type Mercury

# Add data point with auto timestamp (*)
TS.ADD thermometer:1 * 23.5

# Add data point with explicit timestamp
TS.ADD thermometer:1 1626428700000 24.2

# Add multiple data points (MADD)
TS.MADD thermometer:1 1 9.2 thermometer:1 2 9.9 thermometer:2 2 10.3

# Query data
TS.GET thermometer:1
TS.RANGE thermometer:1 - +
TS.RANGE thermometer:1 - + AGGREGATION avg 60000

# Create compaction rule
TS.CREATE thermometer:1:hourly
TS.CREATERULE thermometer:1 thermometer:1:hourly AGGREGATION avg 3600000

# Query with filters
TS.MRANGE - + FILTER location=UK
TS.MRANGE - + FILTER type=Mercury AGGREGATION max 60000
```

## Vector Set Commands

### VADD and VSIM - Store and Search Vectors

Stores vectors for similarity search. Supports KNN queries with filtering.

```bash
# Add vectors to a vector set
VADD points VALUES 2 1.0 1.0 pt:A
VADD points VALUES 2 2.0 2.0 pt:B
VADD points VALUES 2 0.5 0.5 pt:C

# Get vector set info
VCARD points
# Returns: (integer) 3

VDIM points
# Returns: (integer) 2

# Get vector embedding
VEMB points pt:A
# Returns: ["1", "1"]

# Set attributes for filtering
VSETATTR points pt:A '{"size": "large", "price": 25.00}'
VGETATTR points pt:A

# Similarity search
VSIM points VALUES 2 0.9 0.1
VSIM points ELE pt:A WITHSCORES COUNT 4

# Filtered similarity search
VSIM points ELE pt:A FILTER '.size == "large"'
VSIM points ELE pt:A FILTER '.size == "large" && .price > 20.00'
```

## Bloom Filter Commands

### BF.RESERVE and BF.ADD - Probabilistic Set Membership

Creates space-efficient probabilistic data structures for membership testing. Allows false positives but not false negatives.

```bash
# Reserve bloom filter with error rate and capacity
BF.RESERVE bikes:models 0.001 1000000

# Add single item
BF.ADD bikes:models "Smoky Mountain Striker"
# Returns: (integer) 1

# Check if item exists
BF.EXISTS bikes:models "Smoky Mountain Striker"
# Returns: (integer) 1

BF.EXISTS bikes:models "Unknown Bike"
# Returns: (integer) 0 (definitely not present)

# Add multiple items
BF.MADD bikes:models "Rocky Mountain Racer" "Cloudy City Cruiser"

# Check multiple items
BF.MEXISTS bikes:models "Rocky Mountain Racer" "Unknown Model"
# Returns: 1) (integer) 1
#          2) (integer) 0

# Get filter info
BF.INFO bikes:models
```

## Pub/Sub Commands

### PUBLISH and SUBSCRIBE - Message Broadcasting

Implements publish/subscribe messaging pattern for real-time communication between clients.

```bash
# Terminal 1: Subscribe to channel
SUBSCRIBE news

# Terminal 2: Publish message
PUBLISH news "Breaking: Redis 8.0 released!"
# Returns: (integer) 1 (number of subscribers that received the message)

# Pattern subscribe
PSUBSCRIBE news:*
# Receives messages from news:sports, news:tech, etc.

# Using redis-py
import redis
r = redis.Redis()
pubsub = r.pubsub()
pubsub.subscribe('news')

for message in pubsub.listen():
    if message['type'] == 'message':
        print(f"Received: {message['data']}")

# Publishing
r.publish('news', 'Hello subscribers!')
```

## Transactions

### MULTI/EXEC - Atomic Command Execution

Groups commands for atomic execution. All commands succeed or none execute.

```bash
# Start transaction
MULTI

# Queue commands
SET balance:user1 100
DECRBY balance:user1 50
INCRBY balance:user2 50

# Execute atomically
EXEC
# Returns results of all commands

# Watch for optimistic locking
WATCH balance:user1
MULTI
DECRBY balance:user1 50
EXEC
# Returns nil if balance:user1 was modified by another client

# Using redis-py
with r.pipeline() as pipe:
    pipe.set('key1', 'value1')
    pipe.set('key2', 'value2')
    pipe.incr('counter')
    results = pipe.execute()
```

## Lua Scripting

### EVAL - Execute Lua Scripts

Runs Lua scripts atomically on the server. Scripts can access keys and arguments.

```bash
# Simple script
EVAL "return redis.call('GET', KEYS[1])" 1 mykey

# Script with multiple keys and args
EVAL "redis.call('SET', KEYS[1], ARGV[1]); redis.call('SET', KEYS[2], ARGV[2])" 2 key1 key2 value1 value2

# Conditional update script
EVAL "if redis.call('GET', KEYS[1]) == ARGV[1] then return redis.call('DEL', KEYS[1]) else return 0 end" 1 resource-name token-value

# Load and execute script by SHA
SCRIPT LOAD "return redis.call('GET', KEYS[1])"
# Returns: "sha1_hash"
EVALSHA sha1_hash 1 mykey

# Using redis-py
script = r.register_script("""
    local current = redis.call('GET', KEYS[1])
    if current == ARGV[1] then
        return redis.call('DEL', KEYS[1])
    end
    return 0
""")
result = script(keys=['lock'], args=['lock-value'])
```

Redis serves as a versatile data platform for caching, session management, real-time analytics, leaderboards, message queues, rate limiting, and AI/ML applications. Its in-memory architecture delivers sub-millisecond latency, while persistence options (RDB snapshots, AOF logs) ensure durability. The ecosystem supports horizontal scaling through clustering, high availability via replication and Redis Sentinel, and seamless integration with modern application stacks.

Common integration patterns include using Redis as a cache layer in front of slower databases, implementing distributed locks with the Redlock algorithm, building real-time leaderboards with sorted sets, managing user sessions with hashes and expiration, creating event-driven architectures with Streams, and powering vector similarity search for AI applications with RedisVL or the FT.SEARCH command. Redis client libraries provide connection pooling, automatic reconnection, pipeline batching, and client-side caching to optimize performance in production deployments.
