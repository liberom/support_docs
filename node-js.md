# Node.js

Node.js is an open-source, cross-platform JavaScript runtime environment built on Chrome's V8 JavaScript engine. It enables developers to run JavaScript on the server-side, providing an event-driven, non-blocking I/O model that makes it efficient and suitable for building scalable network applications. Node.js includes a rich standard library with modules for HTTP servers/clients, file system operations, streams, cryptography, child processes, and more.

The Node.js platform follows a release schedule with Current and LTS (Long Term Support) versions. Current releases contain the latest features under active development, while LTS releases focus on stability and security. The module system supports both CommonJS (`require()`) and ES Modules (`import`), with modules accessed using the `node:` protocol prefix (e.g., `require('node:fs')`).

---

## HTTP Module - Creating Web Servers

The `node:http` module provides client and server implementations for HTTP protocol. It's designed to support streaming, chunk-encoded messages without buffering entire requests or responses.

```javascript
const http = require('node:http');

// Create an HTTP server
const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'application/json' });
  res.end(JSON.stringify({
    message: 'Hello World',
    url: req.url,
    method: req.method
  }));
});

server.listen(3000, '127.0.0.1', () => {
  console.log('Server running at http://127.0.0.1:3000/');
});

// Making HTTP requests
const options = {
  hostname: 'jsonplaceholder.typicode.com',
  port: 443,
  path: '/posts/1',
  method: 'GET'
};

const req = http.request(options, (res) => {
  let data = '';
  res.on('data', (chunk) => data += chunk);
  res.on('end', () => console.log(JSON.parse(data)));
});

req.on('error', (error) => console.error('Request error:', error.message));
req.end();
```

---

## File System Module - Reading and Writing Files

The `node:fs` module enables interaction with the file system using POSIX-like functions. It provides synchronous, callback-based, and promise-based APIs for all operations.

```javascript
const fs = require('node:fs');
const fsPromises = require('node:fs/promises');

// Synchronous file reading
try {
  const data = fs.readFileSync('/path/to/file.txt', 'utf8');
  console.log(data);
} catch (err) {
  console.error('Error reading file:', err.message);
}

// Callback-based file writing
fs.writeFile('/path/to/output.txt', 'Hello Node.js!', (err) => {
  if (err) throw err;
  console.log('File has been saved!');
});

// Promise-based async/await operations
async function handleFiles() {
  try {
    // Read file
    const content = await fsPromises.readFile('input.txt', 'utf8');

    // Write transformed content
    await fsPromises.writeFile('output.txt', content.toUpperCase());

    // Append to file
    await fsPromises.appendFile('log.txt', `Processed at ${new Date()}\n`);

    // Get file stats
    const stats = await fsPromises.stat('output.txt');
    console.log(`File size: ${stats.size} bytes`);

    // List directory contents
    const files = await fsPromises.readdir('./');
    console.log('Directory contents:', files);
  } catch (error) {
    console.error('File operation failed:', error.message);
  }
}

handleFiles();
```

---

## Path Module - File Path Utilities

The `node:path` module provides utilities for working with file and directory paths. Operations vary based on the operating system, with `path.posix` and `path.win32` available for consistent cross-platform handling.

```javascript
const path = require('node:path');

// Get the last portion of a path
console.log(path.basename('/foo/bar/baz/file.html'));
// Returns: 'file.html'

console.log(path.basename('/foo/bar/baz/file.html', '.html'));
// Returns: 'file'

// Get directory name
console.log(path.dirname('/foo/bar/baz/file.html'));
// Returns: '/foo/bar/baz'

// Get file extension
console.log(path.extname('index.coffee.md'));
// Returns: '.md'

// Join path segments
console.log(path.join('/foo', 'bar', 'baz/asdf', 'quux', '..'));
// Returns: '/foo/bar/baz/asdf'

// Resolve absolute path
console.log(path.resolve('/foo/bar', './baz'));
// Returns: '/foo/bar/baz'

// Parse path into object
const parsed = path.parse('/home/user/dir/file.txt');
console.log(parsed);
// Returns: { root: '/', dir: '/home/user/dir', base: 'file.txt', ext: '.txt', name: 'file' }

// Format path object back to string
const formatted = path.format({
  dir: '/home/user/dir',
  base: 'file.txt'
});
console.log(formatted);
// Returns: '/home/user/dir/file.txt'

// Platform-specific delimiter
console.log(process.env.PATH.split(path.delimiter));
// Returns array of PATH directories
```

---

## Events Module - EventEmitter Pattern

The `node:events` module provides the `EventEmitter` class, which is the foundation for Node.js's event-driven architecture. Many core modules extend EventEmitter.

```javascript
const EventEmitter = require('node:events');

class MyEmitter extends EventEmitter {}

const myEmitter = new MyEmitter();

// Register event listener
myEmitter.on('event', (a, b) => {
  console.log('Event triggered with:', a, b);
});

// Register one-time listener
myEmitter.once('connection', (stream) => {
  console.log('First connection only!');
});

// Error handling (critical - unhandled 'error' events crash Node.js)
myEmitter.on('error', (err) => {
  console.error('An error occurred:', err.message);
});

// Emit events
myEmitter.emit('event', 'arg1', 'arg2');
myEmitter.emit('connection', { id: 1 });
myEmitter.emit('connection', { id: 2 }); // This won't trigger the once listener

// Remove listeners
const callback = () => console.log('Callback');
myEmitter.on('data', callback);
myEmitter.removeListener('data', callback);

// Get listener count
console.log(myEmitter.listenerCount('event'));

// Async iteration with events
const { on } = require('node:events');

async function processEvents() {
  const emitter = new EventEmitter();

  setTimeout(() => {
    emitter.emit('data', 'first');
    emitter.emit('data', 'second');
    emitter.emit('close');
  }, 100);

  for await (const [value] of on(emitter, 'data')) {
    console.log('Received:', value);
    if (value === 'second') break;
  }
}

processEvents();
```

---

## Stream Module - Streaming Data

The `node:stream` module provides an API for implementing streaming data interfaces. Streams are readable, writable, or both (duplex/transform), and are instances of EventEmitter.

```javascript
const { pipeline } = require('node:stream/promises');
const fs = require('node:fs');
const zlib = require('node:zlib');
const { Transform } = require('node:stream');

// Pipeline for stream composition
async function compressFile() {
  await pipeline(
    fs.createReadStream('input.txt'),
    zlib.createGzip(),
    fs.createWriteStream('input.txt.gz')
  );
  console.log('Pipeline succeeded.');
}

compressFile().catch(console.error);

// Using pipeline with async generators
async function processStream() {
  await pipeline(
    fs.createReadStream('data.txt'),
    async function* (source, { signal }) {
      source.setEncoding('utf8');
      for await (const chunk of source) {
        yield chunk.toUpperCase();
      }
    },
    fs.createWriteStream('output.txt')
  );
}

// Creating a custom Transform stream
const upperCaseTransform = new Transform({
  transform(chunk, encoding, callback) {
    this.push(chunk.toString().toUpperCase());
    callback();
  }
});

// Reading streams with for-await-of
const readable = fs.createReadStream('file.txt', { encoding: 'utf8' });

async function readStream() {
  for await (const chunk of readable) {
    console.log('Chunk:', chunk);
  }
}

// Piping streams with abort signal
const { pipeline: pipelineCallback } = require('node:stream');

const ac = new AbortController();
const { signal } = ac;

pipeline(
  fs.createReadStream('source.txt'),
  zlib.createGzip(),
  fs.createWriteStream('dest.txt.gz'),
  { signal }
).catch((err) => {
  if (err.name === 'AbortError') {
    console.log('Pipeline was aborted');
  }
});

// Abort after 1 second
setTimeout(() => ac.abort(), 1000);
```

---

## Child Process Module - Spawning Subprocesses

The `node:child_process` module provides the ability to spawn subprocesses. It offers `spawn()`, `exec()`, `execFile()`, and `fork()` methods for different use cases.

```javascript
const { spawn, exec, execFile, fork } = require('node:child_process');
const util = require('node:util');

// spawn() - for streaming output
const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.error(`stderr: ${data}`);
});

ls.on('close', (code) => {
  console.log(`child process exited with code ${code}`);
});

// exec() - for buffered output with shell
exec('cat *.js | wc -l', (error, stdout, stderr) => {
  if (error) {
    console.error(`exec error: ${error}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.error(`stderr: ${stderr}`);
});

// Promisified exec
const execPromise = util.promisify(exec);

async function runCommand() {
  try {
    const { stdout, stderr } = await execPromise('ls -la');
    console.log('stdout:', stdout);
    if (stderr) console.error('stderr:', stderr);
  } catch (error) {
    console.error('Error:', error.message);
  }
}

runCommand();

// fork() - for Node.js processes with IPC
// parent.js
const child = fork('./child.js');

child.on('message', (message) => {
  console.log('Message from child:', message);
});

child.send({ hello: 'world' });

// child.js (separate file)
// process.on('message', (message) => {
//   console.log('Message from parent:', message);
//   process.send({ response: 'received' });
// });

// execFile() - execute without shell
execFile('node', ['--version'], (error, stdout, stderr) => {
  if (error) throw error;
  console.log('Node version:', stdout);
});
```

---

## Crypto Module - Cryptographic Functions

The `node:crypto` module provides cryptographic functionality including hashing, HMAC, encryption/decryption, and key generation using OpenSSL.

```javascript
const crypto = require('node:crypto');

// Creating hashes
const hash = crypto.createHash('sha256');
hash.update('Hello World');
console.log(hash.digest('hex'));
// Output: a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b57b277d9ad9f146e

// HMAC (Hash-based Message Authentication Code)
const secret = 'my-secret-key';
const hmac = crypto.createHmac('sha256', secret)
  .update('I love cupcakes')
  .digest('hex');
console.log(hmac);
// Output: c0fa1bc00531bd78ef38c628449c5102aeabd49b5dc3a2a516ea6ea959d6658e

// Encryption and decryption
const algorithm = 'aes-256-cbc';
const key = crypto.randomBytes(32);
const iv = crypto.randomBytes(16);

function encrypt(text) {
  const cipher = crypto.createCipheriv(algorithm, key, iv);
  let encrypted = cipher.update(text, 'utf8', 'hex');
  encrypted += cipher.final('hex');
  return encrypted;
}

function decrypt(encryptedText) {
  const decipher = crypto.createDecipheriv(algorithm, key, iv);
  let decrypted = decipher.update(encryptedText, 'hex', 'utf8');
  decrypted += decipher.final('utf8');
  return decrypted;
}

const encrypted = encrypt('Secret message');
console.log('Encrypted:', encrypted);
console.log('Decrypted:', decrypt(encrypted));

// Generate random bytes
const randomBytes = crypto.randomBytes(16).toString('hex');
console.log('Random bytes:', randomBytes);

// Generate UUID
const uuid = crypto.randomUUID();
console.log('UUID:', uuid);

// Password hashing with scrypt
const password = 'user-password';
const salt = crypto.randomBytes(16).toString('hex');

crypto.scrypt(password, salt, 64, (err, derivedKey) => {
  if (err) throw err;
  console.log('Derived key:', derivedKey.toString('hex'));
});
```

---

## Buffer Module - Binary Data Handling

The `Buffer` class is used to handle binary data directly. Buffers are fixed-length sequences of bytes and are subclasses of JavaScript's Uint8Array.

```javascript
const { Buffer } = require('node:buffer');

// Creating buffers
const buf1 = Buffer.alloc(10); // Zero-filled buffer of 10 bytes
const buf2 = Buffer.alloc(10, 1); // Buffer filled with value 1
const buf3 = Buffer.allocUnsafe(10); // Uninitialized (faster but may contain old data)
const buf4 = Buffer.from([1, 2, 3]); // From array
const buf5 = Buffer.from('Hello World'); // From string (UTF-8 default)
const buf6 = Buffer.from('48656c6c6f', 'hex'); // From hex string

// String encoding/decoding
const buf = Buffer.from('hello world', 'utf8');
console.log(buf.toString('hex'));
// Output: 68656c6c6f20776f726c64

console.log(buf.toString('base64'));
// Output: aGVsbG8gd29ybGQ=

// Buffer operations
const buf7 = Buffer.from('Hello');
const buf8 = Buffer.from(' World');
const combined = Buffer.concat([buf7, buf8]);
console.log(combined.toString());
// Output: Hello World

// Slicing and copying
const original = Buffer.from('Hello World');
const slice = original.subarray(0, 5);
console.log(slice.toString()); // Hello

const target = Buffer.alloc(5);
original.copy(target, 0, 0, 5);
console.log(target.toString()); // Hello

// Comparing buffers
const bufA = Buffer.from('ABC');
const bufB = Buffer.from('BCD');
console.log(bufA.compare(bufB)); // -1 (bufA < bufB)
console.log(Buffer.compare(bufA, bufB)); // -1

// Finding in buffers
const searchBuf = Buffer.from('Hello World');
console.log(searchBuf.indexOf('World')); // 6
console.log(searchBuf.includes('World')); // true
```

---

## URL Module - URL Parsing and Formatting

The `node:url` module provides utilities for URL resolution and parsing using the WHATWG URL Standard compatible with web browsers.

```javascript
const { URL, URLSearchParams } = require('node:url');

// Parsing URLs
const myURL = new URL('https://user:pass@example.com:8080/path/name?query=string#hash');

console.log(myURL.hostname);  // example.com
console.log(myURL.pathname);  // /path/name
console.log(myURL.search);    // ?query=string
console.log(myURL.hash);      // #hash
console.log(myURL.port);      // 8080
console.log(myURL.protocol);  // https:
console.log(myURL.origin);    // https://example.com:8080
console.log(myURL.href);      // Full URL string

// Constructing URLs
const newURL = new URL('https://example.org');
newURL.pathname = '/a/b/c';
newURL.search = '?d=e';
newURL.hash = '#fgh';
console.log(newURL.href);
// Output: https://example.org/a/b/c?d=e#fgh

// Relative URL resolution
const base = new URL('https://example.org/foo/bar');
const relative = new URL('../baz', base);
console.log(relative.href);
// Output: https://example.org/baz

// Working with search params
const params = new URLSearchParams('user=abc&query=xyz');
params.append('page', '1');
params.set('user', 'newuser');
params.delete('query');

console.log(params.toString()); // user=newuser&page=1
console.log(params.get('user')); // newuser
console.log(params.has('page')); // true

// Iterating search params
for (const [key, value] of params) {
  console.log(`${key}: ${value}`);
}

// File URLs
const { fileURLToPath, pathToFileURL } = require('node:url');

const filePath = fileURLToPath('file:///home/user/project/file.txt');
console.log(filePath); // /home/user/project/file.txt

const fileUrl = pathToFileURL('/home/user/project/file.txt');
console.log(fileUrl.href); // file:///home/user/project/file.txt
```

---

## Worker Threads - Parallel JavaScript Execution

The `node:worker_threads` module enables parallel JavaScript execution using threads. Unlike child processes, workers can share memory through SharedArrayBuffer.

```javascript
const {
  Worker,
  isMainThread,
  parentPort,
  workerData,
  MessageChannel
} = require('node:worker_threads');

if (isMainThread) {
  // Main thread code
  const worker = new Worker(__filename, {
    workerData: { start: 0, end: 1000000 }
  });

  worker.on('message', (result) => {
    console.log('Sum from worker:', result);
  });

  worker.on('error', (error) => {
    console.error('Worker error:', error);
  });

  worker.on('exit', (code) => {
    if (code !== 0) {
      console.error(`Worker stopped with exit code ${code}`);
    }
  });

  // Using MessageChannel for bidirectional communication
  const { port1, port2 } = new MessageChannel();

  const worker2 = new Worker(__filename, {
    workerData: { type: 'channel' }
  });

  worker2.postMessage({ port: port2 }, [port2]);
  port1.on('message', (msg) => console.log('Received:', msg));
  port1.postMessage('Hello from main thread!');

} else {
  // Worker thread code
  if (workerData.type === 'channel') {
    parentPort.once('message', ({ port }) => {
      port.on('message', (msg) => {
        port.postMessage(`Worker received: ${msg}`);
      });
    });
  } else {
    // CPU-intensive calculation
    const { start, end } = workerData;
    let sum = 0;
    for (let i = start; i <= end; i++) {
      sum += i;
    }
    parentPort.postMessage(sum);
  }
}

// Worker pool pattern example
class WorkerPool {
  constructor(workerScript, numWorkers) {
    this.workers = [];
    this.queue = [];

    for (let i = 0; i < numWorkers; i++) {
      const worker = new Worker(workerScript);
      worker.busy = false;
      this.workers.push(worker);
    }
  }

  runTask(data) {
    return new Promise((resolve, reject) => {
      const worker = this.workers.find(w => !w.busy);
      if (worker) {
        worker.busy = true;
        worker.once('message', (result) => {
          worker.busy = false;
          resolve(result);
        });
        worker.once('error', reject);
        worker.postMessage(data);
      } else {
        this.queue.push({ data, resolve, reject });
      }
    });
  }
}
```

---

## Test Runner - Built-in Testing

The `node:test` module provides a built-in test runner with support for subtests, hooks, mocking, and various assertion styles.

```javascript
const test = require('node:test');
const assert = require('node:assert');

// Basic test
test('synchronous passing test', (t) => {
  assert.strictEqual(1, 1);
});

// Async test
test('asynchronous passing test', async (t) => {
  const result = await Promise.resolve(42);
  assert.strictEqual(result, 42);
});

// Test with subtests
test('top level test', async (t) => {
  await t.test('subtest 1', (t) => {
    assert.strictEqual(1, 1);
  });

  await t.test('subtest 2', (t) => {
    assert.strictEqual(2, 2);
  });
});

// describe/it syntax (BDD style)
const { describe, it, beforeEach, afterEach } = require('node:test');

describe('Math operations', () => {
  let value;

  beforeEach(() => {
    value = 0;
  });

  afterEach(() => {
    value = null;
  });

  it('should add numbers correctly', () => {
    value = 1 + 2;
    assert.strictEqual(value, 3);
  });

  it('should multiply numbers correctly', () => {
    value = 2 * 3;
    assert.strictEqual(value, 6);
  });

  describe('nested suite', () => {
    it('should handle division', () => {
      assert.strictEqual(10 / 2, 5);
    });
  });
});

// Skipping and only tests
test('skipped test', { skip: true }, (t) => {
  // This test is skipped
});

test('conditional skip', { skip: process.platform === 'win32' }, (t) => {
  // Skipped on Windows
});

test.only('only this test runs', (t) => {
  assert.ok(true);
});

// Mocking
const { mock } = require('node:test');

test('mocking example', (t) => {
  const fn = mock.fn((x) => x * 2);

  assert.strictEqual(fn(2), 4);
  assert.strictEqual(fn.mock.calls.length, 1);
  assert.deepStrictEqual(fn.mock.calls[0].arguments, [2]);
});

// Run tests: node --test test.js
```

---

## Util Module - Utility Functions

The `node:util` module provides various utility functions for debugging, formatting, and converting between callback and promise styles.

```javascript
const util = require('node:util');

// Promisify callback-based functions
const fs = require('node:fs');
const readFile = util.promisify(fs.readFile);

async function readConfig() {
  try {
    const content = await readFile('config.json', 'utf8');
    return JSON.parse(content);
  } catch (err) {
    console.error('Error reading config:', err.message);
  }
}

// Callbackify promise-based functions
async function getData() {
  return { message: 'Hello World' };
}

const getDataCallback = util.callbackify(getData);
getDataCallback((err, result) => {
  if (err) throw err;
  console.log(result);
});

// Debug logging
const debug = util.debuglog('myapp');
debug('Debug message: %d', 42);
// Run with NODE_DEBUG=myapp to see output

// Object inspection
const obj = {
  name: 'test',
  nested: { deep: { value: 42 } },
  circular: null
};
obj.circular = obj;

console.log(util.inspect(obj, {
  depth: null,
  colors: true,
  showHidden: false
}));

// Format strings
console.log(util.format('%s: %d', 'count', 42));
// Output: count: 42

// Type checking
console.log(util.types.isPromise(Promise.resolve()));  // true
console.log(util.types.isAsyncFunction(async () => {})); // true
console.log(util.types.isDate(new Date()));  // true
console.log(util.types.isRegExp(/abc/));  // true

// Deprecation warnings
const deprecatedFn = util.deprecate(
  () => console.log('old function'),
  'deprecatedFn() is deprecated. Use newFn() instead.'
);
```

---

## Net Module - TCP/IPC Networking

The `node:net` module provides an asynchronous network API for creating TCP and IPC servers and clients.

```javascript
const net = require('node:net');

// TCP Server
const server = net.createServer((socket) => {
  console.log('Client connected');

  socket.on('data', (data) => {
    console.log('Received:', data.toString());
    socket.write('Echo: ' + data);
  });

  socket.on('end', () => {
    console.log('Client disconnected');
  });

  socket.on('error', (err) => {
    console.error('Socket error:', err.message);
  });
});

server.listen(8080, '127.0.0.1', () => {
  console.log('Server listening on port 8080');
});

// TCP Client
const client = net.createConnection({ port: 8080 }, () => {
  console.log('Connected to server');
  client.write('Hello Server!');
});

client.on('data', (data) => {
  console.log('Server response:', data.toString());
  client.end();
});

client.on('end', () => {
  console.log('Disconnected from server');
});

// IP Address blocking
const blockList = new net.BlockList();
blockList.addAddress('192.168.1.100');
blockList.addRange('10.0.0.1', '10.0.0.100');
blockList.addSubnet('172.16.0.0', 16);

console.log(blockList.check('192.168.1.100')); // true
console.log(blockList.check('8.8.8.8')); // false

// Server with connection handling
const serverWithOptions = net.createServer({
  allowHalfOpen: false,
  pauseOnConnect: false
});

serverWithOptions.maxConnections = 100;

serverWithOptions.on('connection', (socket) => {
  socket.setTimeout(30000);
  socket.setKeepAlive(true, 10000);
});

serverWithOptions.on('error', (err) => {
  if (err.code === 'EADDRINUSE') {
    console.log('Port in use, retrying...');
    setTimeout(() => {
      serverWithOptions.close();
      serverWithOptions.listen(8081);
    }, 1000);
  }
});
```

---

Node.js is primarily used for building web servers, REST APIs, real-time applications (chat, gaming), microservices, command-line tools, and automation scripts. Its non-blocking I/O model makes it excellent for I/O-heavy applications like file processing, database operations, and network services. The extensive npm ecosystem provides packages for virtually any use case.

Common integration patterns include using Express.js or Fastify for web frameworks, connecting to databases with drivers like `pg` (PostgreSQL), `mongoose` (MongoDB), or `mysql2`, and deploying as containerized applications or serverless functions. Node.js integrates well with message queues (Redis, RabbitMQ), cloud services (AWS, GCP, Azure), and CI/CD pipelines, making it a versatile choice for modern application development.
