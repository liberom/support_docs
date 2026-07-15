# Neovim

Neovim is a modern, extensible text editor that aggressively refactors Vim to enable advanced UIs, maximize extensibility, and simplify maintenance. It provides a powerful MessagePack-RPC API that allows external processes, plugins, and scripts to control the editor programmatically, supporting languages including C/C++, Python, Ruby, JavaScript/Node.js, Lua, and many others. The editor maintains compatibility with most Vim plugins while introducing modern features like asynchronous job control, embedded terminal emulation, Lua scripting, Language Server Protocol (LSP) support, native snippet expansion, inline completion for AI-powered suggestions, and a built-in package manager.

The architecture separates concerns into distinct subsystems: the C API layer handles external communication via MessagePack-RPC, the Lua integration provides high-performance scripting capabilities, and the plugin system enables extensibility through both autoloaded scripts and runtime modules. Neovim's event-driven architecture uses libuv for asynchronous I/O, allowing non-blocking operations while maintaining a single-threaded event loop for safe state management. The built-in LSP client, TreeSitter integration, diagnostic framework, snippet engine, and package manager provide modern IDE-like features without requiring external dependencies.

## API Functions

### Buffer Line Operations

Get or set lines from a buffer with zero-based indexing and end-exclusive ranges.

```lua
-- Get all lines from current buffer
local lines = vim.api.nvim_buf_get_lines(0, 0, -1, false)

-- Set lines 5-10 (replacing them)
vim.api.nvim_buf_set_lines(0, 5, 10, false, {
  "function hello()",
  "  print('Hello, World!')",
  "end"
})

-- Insert lines at beginning without replacing
vim.api.nvim_buf_set_lines(0, 0, 0, false, {"-- New header comment"})

-- Get line count
local count = vim.api.nvim_buf_line_count(0)
print("Buffer has " .. count .. " lines")

-- Check if buffer is loaded
if vim.api.nvim_buf_is_loaded(0) then
  print("Buffer is loaded in memory")
end
```

### Buffer Update Events

Attach callbacks to receive real-time notifications of buffer changes.

```lua
-- Capture all buffer updates in a table
local events = {}
vim.api.nvim_buf_attach(0, false, {
  on_lines = function(event, bufnr, changedtick, firstline, lastline, new_lastline, byte_count)
    table.insert(events, {
      type = "lines",
      buffer = bufnr,
      tick = changedtick,
      first = firstline,
      last = lastline,
      new_last = new_lastline,
      bytes = byte_count
    })
  end,
  on_bytes = function(event, bufnr, changedtick, start_row, start_col, byte_offset,
                      old_end_row, old_end_col, old_byte_len,
                      new_end_row, new_end_col, new_byte_len)
    table.insert(events, {
      type = "bytes",
      buffer = bufnr,
      changes = {
        start = {start_row, start_col},
        old_end = {old_end_row, old_end_col},
        new_end = {new_end_row, new_end_col}
      }
    })
  end,
  on_detach = function(event, bufnr)
    print("Detached from buffer " .. bufnr)
  end
})

-- Later: inspect captured events
vim.print(events)
```

### Window and Cursor Management

Control window properties, cursor position, and window configuration.

```lua
-- Get current cursor position (1-based line, 0-based column)
local cursor = vim.api.nvim_win_get_cursor(0)
print(string.format("Line %d, Column %d", cursor[1], cursor[2]))

-- Set cursor to line 10, column 5
vim.api.nvim_win_set_cursor(0, {10, 5})

-- Get window dimensions
local width = vim.api.nvim_win_get_width(0)
local height = vim.api.nvim_win_get_height(0)

-- Open floating window
local buf = vim.api.nvim_create_buf(false, true)  -- not listed, scratch buffer
vim.api.nvim_buf_set_lines(buf, 0, -1, false, {"Floating window content", "Line 2"})

local win = vim.api.nvim_open_win(buf, true, {
  relative = 'editor',
  width = 40,
  height = 10,
  col = 10,
  row = 5,
  style = 'minimal',
  border = 'rounded'
})

-- Get current buffer in window
local current_buf = vim.api.nvim_win_get_buf(0)

-- List all windows
local windows = vim.api.nvim_list_wins()
for _, win_id in ipairs(windows) do
  print("Window ID: " .. win_id)
end
```

### Highlight Groups

Define and retrieve highlight group definitions.

```lua
-- Set a highlight group
vim.api.nvim_set_hl(0, 'MyHighlight', {
  fg = '#ff0000',
  bg = '#000000',
  bold = true,
  italic = true
})

-- Link one highlight group to another
vim.api.nvim_set_hl(0, 'MyLink', { link = 'Comment' })

-- Get highlight definition
local hl = vim.api.nvim_get_hl(0, { name = 'MyHighlight' })
vim.print(hl)  -- { fg = 16711680, bg = 0, bold = true, italic = true }

-- Get all highlight groups
local all_highlights = vim.api.nvim_get_hl(0, {})
for name, definition in pairs(all_highlights) do
  print(name .. " -> " .. vim.inspect(definition))
end

-- Get highlight ID by name
local hl_id = vim.api.nvim_get_hl_id_by_name('Comment')
```

### Autocommands

Create, manage, and trigger autocommands programmatically.

```lua
-- Create an autocommand
local au_id = vim.api.nvim_create_autocmd('TextYankPost', {
  desc = 'Highlight when yanking text',
  callback = function()
    vim.hl.on_yank({ higroup = 'IncSearch', timeout = 200 })
  end
})

-- Create autocommand with pattern
vim.api.nvim_create_autocmd('BufWritePre', {
  pattern = '*.lua',
  callback = function(args)
    print("Saving Lua file: " .. args.file)
    -- Auto-format before save
    vim.lsp.buf.format({ timeout_ms = 2000 })
  end
})

-- Create augroup and multiple autocommands
local group = vim.api.nvim_create_augroup('MyGroup', { clear = true })
vim.api.nvim_create_autocmd({'BufEnter', 'BufWinEnter'}, {
  group = group,
  pattern = '*.py',
  command = 'set expandtab tabstop=4 shiftwidth=4'
})

-- Execute autocommands manually
vim.api.nvim_exec_autocmds('User', { pattern = 'MyCustomEvent', data = { key = 'value' } })

-- Get all autocommands
local autocmds = vim.api.nvim_get_autocmds({ group = group })
vim.print(autocmds)

-- Delete autocommand
vim.api.nvim_del_autocmd(au_id)
```

### Keymaps

Set and manage keyboard mappings across different modes.

```lua
-- Set keymap for normal mode
vim.api.nvim_set_keymap('n', '<leader>w', ':w<CR>', {
  noremap = true,
  silent = true,
  desc = 'Save file'
})

-- Set keymap with Lua callback
vim.keymap.set('n', '<leader>f', function()
  print("Custom function called")
  vim.lsp.buf.format()
end, { desc = 'Format buffer' })

-- Set keymap for multiple modes
vim.keymap.set({'n', 'v'}, '<leader>y', '"+y', { desc = 'Yank to system clipboard' })

-- Buffer-specific keymap
vim.api.nvim_buf_set_keymap(0, 'n', '<leader>r', ':!python %<CR>', {
  noremap = true,
  silent = true
})

-- Get keymaps for a mode
local keymaps = vim.api.nvim_get_keymap('n')
for _, map in ipairs(keymaps) do
  print(map.lhs .. " -> " .. (map.rhs or ""))
end

-- Delete keymap
vim.api.nvim_del_keymap('n', '<leader>w')
vim.keymap.del('n', '<leader>f')
```

### User Commands

Create custom Ex commands with completion and arguments.

```lua
-- Simple command
vim.api.nvim_create_user_command('Hello', function()
  print('Hello, World!')
end, {})

-- Command with arguments
vim.api.nvim_create_user_command('Greet', function(opts)
  print('Hello, ' .. opts.args .. '!')
end, { nargs = 1 })

-- Command with completion
vim.api.nvim_create_user_command('EditConfig', function(opts)
  vim.cmd.edit('~/.config/nvim/' .. opts.args)
end, {
  nargs = 1,
  complete = function(arg_lead, cmdline, cursor_pos)
    local files = vim.fn.glob('~/.config/nvim/' .. arg_lead .. '*', false, true)
    return vim.tbl_map(function(f)
      return vim.fn.fnamemodify(f, ':t')
    end, files)
  end
})

-- Command with range
vim.api.nvim_create_user_command('LineCount', function(opts)
  local count = opts.line2 - opts.line1 + 1
  print(string.format('Selected %d lines', count))
end, { range = true })

-- Buffer-local command
vim.api.nvim_buf_create_user_command(0, 'LocalCommand', function()
  print('Command for buffer ' .. vim.api.nvim_get_current_buf())
end, {})

-- Delete command
vim.api.nvim_del_user_command('Hello')
```

### Vimscript Execution

Execute Vimscript code and evaluate expressions.

```lua
-- Execute single command
vim.api.nvim_command('set number')

-- Execute multiple commands with output capture
local result = vim.api.nvim_exec2([[
  let g:my_var = 42
  function! MyFunc()
    return g:my_var * 2
  endfunction
  echo MyFunc()
]], { output = true })
print(result.output)  -- "84"

-- Execute Lua code from API
local lua_result = vim.api.nvim_exec_lua([[
  local sum = 0
  for i = 1, 10 do
    sum = sum + i
  end
  return sum
]], {})
print(lua_result)  -- 55

-- Evaluate expression
local value = vim.api.nvim_eval('exists("g:my_var")')
print(value)  -- 1 (true)

-- Call Vimscript function
local result = vim.api.nvim_call_function('expand', {'%:p'})
print("Full path: " .. result)

-- Parse and execute Ex command
local parsed = vim.api.nvim_parse_cmd('split | edit test.txt', {})
vim.api.nvim_cmd(parsed, {})
```

### Variables

Get and set variables in different scopes.

```lua
-- Global variables (g:)
vim.api.nvim_set_var('my_plugin_enabled', true)
local enabled = vim.api.nvim_get_var('my_plugin_enabled')

-- Delete global variable
vim.api.nvim_del_var('my_plugin_enabled')

-- Vim variables (v:)
local count = vim.api.nvim_get_vvar('count')
local servername = vim.api.nvim_get_vvar('servername')

-- Buffer variables (b:)
vim.api.nvim_buf_set_var(0, 'buffer_local', 'value')
local val = vim.api.nvim_buf_get_var(0, 'buffer_local')
vim.api.nvim_buf_del_var(0, 'buffer_local')

-- Window variables (w:)
vim.api.nvim_win_set_var(0, 'window_local', 123)
local num = vim.api.nvim_win_get_var(0, 'window_local')

-- Tabpage variables (t:)
vim.api.nvim_tabpage_set_var(0, 'tab_local', {1, 2, 3})
local list = vim.api.nvim_tabpage_get_var(0, 'tab_local')

-- Options (vim.o, vim.bo, vim.wo)
vim.o.number = true
vim.bo.filetype = 'lua'
vim.wo.wrap = false
```

### Extended Marks (Extmarks)

Create positioned marks with metadata for decorations and tracking.

```lua
-- Create namespace
local ns_id = vim.api.nvim_create_namespace('my_plugin')

-- Set extmark at line 5, column 0
local mark_id = vim.api.nvim_buf_set_extmark(0, ns_id, 4, 0, {
  end_line = 4,
  end_col = 10,
  hl_group = 'Error',
  virt_text = {{'← Error here', 'ErrorMsg'}},
  virt_text_pos = 'eol'
})

-- Get extmark position
local mark = vim.api.nvim_buf_get_extmark_by_id(0, ns_id, mark_id, { details = true })
print(vim.inspect(mark))  -- {4, 0, {end_row = 4, end_col = 10, ...}}

-- Get all extmarks in range
local marks = vim.api.nvim_buf_get_extmarks(0, ns_id, 0, -1, { details = true })
for _, mark_data in ipairs(marks) do
  local id, row, col, details = mark_data[1], mark_data[2], mark_data[3], mark_data[4]
  print(string.format("Mark %d at line %d, col %d", id, row, col))
end

-- Delete extmark
vim.api.nvim_buf_del_extmark(0, ns_id, mark_id)

-- Clear all extmarks in namespace
vim.api.nvim_buf_clear_namespace(0, ns_id, 0, -1)
```

### Input and Feedkeys

Send input and keyboard events to Neovim.

```lua
-- Feed keys as if typed
vim.api.nvim_feedkeys('iHello', 'n', false)

-- Feed keys with special key codes
vim.api.nvim_feedkeys(vim.api.nvim_replace_termcodes('<Esc>:w<CR>', true, false, true), 'n', false)

-- Input text (processes special keys)
vim.api.nvim_input('Gdd')  -- Go to last line and delete it

-- Input mouse event
vim.api.nvim_input_mouse('left', 'press', '', 0, 10, 20)

-- Put text at cursor
vim.api.nvim_put({'line 1', 'line 2'}, 'l', true, true)
```

### RPC and Channels

Communicate with external processes via RPC channels.

```lua
-- Start job with RPC enabled
local job_id = vim.fn.jobstart({'python3', '-u', 'server.py'}, {
  rpc = true,
  on_exit = function(id, code, event)
    print("Job exited with code: " .. code)
  end
})

-- Send RPC request (blocking)
local response = vim.fn.rpcrequest(job_id, 'method_name', {arg1 = 'value'})
print(vim.inspect(response))

-- Send RPC notification (non-blocking)
vim.fn.rpcnotify(job_id, 'notification', 'data')

-- List all channels
local channels = vim.api.nvim_list_chans()
for _, chan in ipairs(channels) do
  print(string.format("Channel %d: %s", chan.id, chan.mode))
end

-- Get channel info
local info = vim.api.nvim_get_chan_info(job_id)
vim.print(info)

-- Stop job
vim.fn.jobstop(job_id)
```

### LSP Client Integration

Start and manage Language Server Protocol clients.

```lua
-- Start LSP client
vim.lsp.start({
  name = 'my-language-server',
  cmd = {'language-server', '--stdio'},
  root_dir = vim.fs.dirname(vim.fs.find({'package.json', '.git'}, { upward = true })[1]),
  capabilities = vim.lsp.protocol.make_client_capabilities(),
  on_attach = function(client, bufnr)
    print("LSP attached to buffer " .. bufnr)

    -- Enable completion
    vim.bo[bufnr].omnifunc = 'v:lua.vim.lsp.omnifunc'

    -- Buffer-local keymaps
    vim.keymap.set('n', 'gd', vim.lsp.buf.definition, { buffer = bufnr })
    vim.keymap.set('n', 'K', vim.lsp.buf.hover, { buffer = bufnr })
    vim.keymap.set('n', '<leader>rn', vim.lsp.buf.rename, { buffer = bufnr })
    vim.keymap.set('n', '<leader>ca', vim.lsp.buf.code_action, { buffer = bufnr })
  end
})

-- Get active clients
local clients = vim.lsp.get_clients({ bufnr = 0 })
for _, client in ipairs(clients) do
  print(client.name .. " (id: " .. client.id .. ")")
end

-- Send LSP request
local result = vim.lsp.buf_request_sync(0, 'textDocument/hover',
  vim.lsp.util.make_position_params(), 1000)
if result then
  for client_id, response in pairs(result) do
    if response.result then
      vim.print(response.result)
    end
  end
end

-- Stop LSP client
vim.lsp.stop_client(client_id)
```

### LSP Inline Completion

Use LSP servers for inline completions (Copilot-style multiline suggestions).

```lua
-- Enable inline completion (usually in init.lua)
vim.lsp.inline_completion.enable()

-- Or enable for specific buffer
vim.lsp.inline_completion.enable({ bufnr = 0 })

-- Manually trigger inline completion
vim.lsp.inline_completion.get()

-- Accept the current inline completion
vim.lsp.inline_completion.accept()

-- Cycle to next/previous completion
vim.lsp.inline_completion.select_next()
vim.lsp.inline_completion.select_prev()

-- Cancel current completion
vim.lsp.inline_completion.cancel()

-- Example: Configure with GitHub Copilot
vim.lsp.config('copilot', {
  cmd = { 'copilot-language-server', '--stdio' },
  root_markers = { '.git' },
})
vim.lsp.enable('copilot')
vim.lsp.inline_completion.enable()

-- Set up keymaps
vim.keymap.set('i', '<C-y>', vim.lsp.inline_completion.accept)
vim.keymap.set('i', '<C-n>', vim.lsp.inline_completion.select_next)
vim.keymap.set('i', '<C-p>', vim.lsp.inline_completion.select_prev)
```

### LSP Inlay Hints

Display inline hints for parameters, types, and other contextual information.

```lua
-- Enable inlay hints for current buffer
vim.lsp.inlay_hint.enable(true)

-- Disable inlay hints
vim.lsp.inlay_hint.enable(false)

-- Check if inlay hints are enabled
local enabled = vim.lsp.inlay_hint.is_enabled({ bufnr = 0 })

-- Toggle inlay hints
vim.keymap.set('n', '<leader>h', function()
  vim.lsp.inlay_hint.enable(not vim.lsp.inlay_hint.is_enabled())
end)

-- Example: Enable inlay hints automatically on LSP attach
vim.api.nvim_create_autocmd('LspAttach', {
  callback = function(args)
    local client = vim.lsp.get_client_by_id(args.data.client_id)
    if client and client.server_capabilities.inlayHintProvider then
      vim.lsp.inlay_hint.enable(true, { bufnr = args.buf })
    end
  end
})
```

### Diagnostics

Display and manage diagnostic messages (errors, warnings, hints).

```lua
-- Set diagnostics for buffer
vim.diagnostic.set(vim.api.nvim_create_namespace('my_linter'), 0, {
  {
    lnum = 5,
    col = 10,
    end_lnum = 5,
    end_col = 15,
    severity = vim.diagnostic.severity.ERROR,
    message = "Undefined variable 'foo'",
    source = "my_linter"
  },
  {
    lnum = 10,
    col = 0,
    severity = vim.diagnostic.severity.WARN,
    message = "Unused variable 'bar'"
  }
}, {})

-- Get diagnostics
local diagnostics = vim.diagnostic.get(0)
for _, diag in ipairs(diagnostics) do
  print(string.format("Line %d: %s", diag.lnum + 1, diag.message))
end

-- Configure diagnostic display
vim.diagnostic.config({
  virtual_text = {
    prefix = '■',
    spacing = 4,
  },
  signs = true,
  underline = true,
  update_in_insert = false,
  severity_sort = true,
})

-- Navigate diagnostics
vim.diagnostic.goto_next()
vim.diagnostic.goto_prev()

-- Show diagnostics in floating window
vim.diagnostic.open_float(nil, { focus = false })
```

### TreeSitter Integration

Parse and query code syntax trees.

```lua
-- Get parser for current buffer
local parser = vim.treesitter.get_parser(0, 'lua')

-- Parse buffer
local tree = parser:parse()[1]
local root = tree:root()

-- Query syntax nodes
local query = vim.treesitter.query.parse('lua', [[
  (function_declaration
    name: (identifier) @function.name
    parameters: (parameters) @function.params)
]])

for id, node, metadata in query:iter_captures(root, 0, 0, -1) do
  local name = query.captures[id]
  local text = vim.treesitter.get_node_text(node, 0)
  print(string.format("%s: %s", name, text))
end

-- Get node at cursor
local node = vim.treesitter.get_node()
if node then
  print("Node type: " .. node:type())
  print("Node range: " .. vim.inspect({node:range()}))
end

-- Highlight with TreeSitter
vim.treesitter.start(0, 'lua')
vim.treesitter.stop(0)
```

## RPC API Access

### Python Client

Connect to Neovim from Python using MessagePack-RPC.

```python
from pynvim import attach

# Connect to running instance
nvim = attach('socket', path='/tmp/nvim.sock')

# Or start embedded instance
nvim = attach('child', argv=['nvim', '--embed', '--headless'])

# Call API functions
nvim.command('echo "Hello from Python"')
buffers = nvim.buffers
current = nvim.current.buffer
lines = current[:]  # Get all lines

# Set buffer content
current[:] = ['# New content', 'print("Hello")']

# Evaluate expressions
result = nvim.eval('2 + 2')
print(result)  # 4

# Call Vimscript functions
path = nvim.call('expand', '%:p')

# Execute Lua
result = nvim.exec_lua('return vim.api.nvim_list_bufs()', [])
print(result)

# Close connection
nvim.close()
```

### Node.js Client

Use the neovim npm package for JavaScript/TypeScript integration.

```javascript
const { attach } = require('neovim');
const net = require('net');

// Connect via socket
const socket = net.connect('/tmp/nvim.sock');
const nvim = attach({ socket });

// Or via stdio
const { spawn } = require('child_process');
const proc = spawn('nvim', ['--embed', '--headless'], {});
const nvim = attach({ proc });

// Call API methods
(async () => {
  const buffers = await nvim.buffers;
  console.log(`Buffer count: ${buffers.length}`);

  const current = await nvim.buffer;
  const lines = await current.lines;
  console.log(lines);

  // Execute commands
  await nvim.command('echo "Hello from Node.js"');

  // Execute Lua
  const result = await nvim.lua(`
    return vim.api.nvim_get_current_line()
  `);
  console.log(result);

  // Listen for events
  nvim.on('notification', (method, args) => {
    console.log(`Notification: ${method}`, args);
  });

  await nvim.quit();
})();
```

### Ruby Client

Access Neovim via Ruby with the neovim gem.

```ruby
require 'neovim'

# Connect to socket
client = Neovim.attach_unix('/tmp/nvim.sock')

# Or start embedded
client = Neovim.attach_child(['nvim', '--embed', '--headless'])

# Execute commands
client.command('echo "Hello from Ruby"')

# Get and set lines
buffer = client.get_current_buf
lines = buffer.get_lines(0, -1, false)
buffer.set_lines(0, -1, false, ['# New content', 'puts "Hello"'])

# Evaluate expressions
count = client.eval('line("$")')
puts "Line count: #{count}"

# Call Vimscript functions
path = client.call_function('expand', ['%:p'])

# Execute Lua
result = client.exec_lua('return vim.bo.filetype', [])
puts "Filetype: #{result}"
```

### Command Line via curl

Access Neovim through TCP socket using any HTTP client.

```bash
# Start Neovim with TCP listener
nvim --listen 127.0.0.1:6666

# Send RPC call via netcat (MessagePack format)
# Format: [type, msgid, method, params]
echo '[0, 1, "nvim_command", ["echo \"Hello\""]]' | \
  msgpack2json -d | \
  nc 127.0.0.1 6666

# Or use a Python one-liner
python3 << 'EOF'
import msgpack, socket
sock = socket.socket()
sock.connect(('127.0.0.1', 6666))
request = msgpack.packb([0, 1, 'nvim_exec2', ['echo "Hello"', {'output': True}]])
sock.send(request)
response = msgpack.unpackb(sock.recv(4096))
print(response)  # [1, msgid, error, result]
sock.close()
EOF

# Using pynvim for simpler access
python3 -c "
from pynvim import attach
nvim = attach('tcp', address='127.0.0.1', port=6666)
print(nvim.command_output('version'))
nvim.close()
"
```

### Remote Plugin (Python)

Create a remote plugin that extends Neovim functionality.

```python
# rplugin/python3/my_plugin.py
import pynvim

@pynvim.plugin
class MyPlugin:
    def __init__(self, nvim):
        self.nvim = nvim

    @pynvim.command('HelloWorld', nargs='*', sync=True)
    def hello_command(self, args):
        self.nvim.out_write('Hello, World!\n')

    @pynvim.function('MyFunction', sync=True)
    def my_function(self, args):
        return f"You passed: {args}"

    @pynvim.autocmd('BufEnter', pattern='*.py', sync=True)
    def on_buf_enter(self):
        self.nvim.out_write('Entered Python buffer\n')

# Update remote plugins
# :UpdateRemotePlugins
# Then restart Neovim and use :HelloWorld
```

## Configuration

### Basic Init Configuration

Essential Neovim configuration using Lua.

```lua
-- ~/.config/nvim/init.lua

-- Set leader key
vim.g.mapleader = ' '

-- Options
vim.o.number = true
vim.o.relativenumber = true
vim.o.ignorecase = true
vim.o.smartcase = true
vim.o.expandtab = true
vim.o.shiftwidth = 2
vim.o.tabstop = 2
vim.o.cursorline = true
vim.o.scrolloff = 10
vim.o.clipboard = 'unnamedplus'
vim.o.termguicolors = true

-- Keymaps
vim.keymap.set('t', '<Esc>', '<C-\\><C-n>')
vim.keymap.set('n', '<leader>w', ':w<CR>')
vim.keymap.set('n', '<leader>q', ':q<CR>')
vim.keymap.set({'n', 'v'}, '<leader>y', '"+y')
vim.keymap.set('n', '<C-h>', '<C-w>h')
vim.keymap.set('n', '<C-j>', '<C-w>j')
vim.keymap.set('n', '<C-k>', '<C-w>k')
vim.keymap.set('n', '<C-l>', '<C-w>l')

-- Autocommands
vim.api.nvim_create_autocmd('TextYankPost', {
  callback = function()
    vim.hl.on_yank({ timeout = 200 })
  end
})

vim.api.nvim_create_autocmd('FileType', {
  pattern = 'python',
  callback = function()
    vim.bo.expandtab = true
    vim.bo.shiftwidth = 4
    vim.bo.tabstop = 4
  end
})

-- User commands
vim.api.nvim_create_user_command('GitBlameLine', function()
  local line = vim.fn.line('.')
  local file = vim.api.nvim_buf_get_name(0)
  local result = vim.system({'git', 'blame', '-L', line .. ',+1', file}):wait()
  print(result.stdout)
end, {})
```

### Native Snippet Support

Expand and navigate through snippets using the built-in snippet engine.

```lua
-- Expand a snippet at cursor
vim.snippet.expand("function ${1:name}($2)\n  $0\nend")

-- Navigate to next/previous tabstop
vim.snippet.jump(1)   -- Next tabstop
vim.snippet.jump(-1)  -- Previous tabstop

-- Check if in an active snippet
if vim.snippet.active() then
  print("Currently in a snippet")
end

-- Stop the current snippet session
vim.snippet.stop()

-- Example: Set up Tab and S-Tab for snippet navigation
vim.keymap.set({'i', 's'}, '<Tab>', function()
  if vim.snippet.active({ direction = 1 }) then
    return '<Cmd>lua vim.snippet.jump(1)<CR>'
  else
    return '<Tab>'
  end
end, { expr = true })

vim.keymap.set({'i', 's'}, '<S-Tab>', function()
  if vim.snippet.active({ direction = -1 }) then
    return '<Cmd>lua vim.snippet.jump(-1)<CR>'
  else
    return '<S-Tab>'
  end
end, { expr = true })
```

### Plugin Management

Use the built-in vim.pack package manager or external plugin managers.

```lua
-- Using built-in vim.pack (experimental but stable)
vim.pack.add({
  'https://github.com/neovim/nvim-lspconfig',
  'https://github.com/nvim-treesitter/nvim-treesitter',

  -- Specify version constraints
  {
    src = 'https://github.com/user/plugin',
    version = vim.version.range('1.0'),  -- Semver constraint
  },

  -- Use specific branch or commit
  {
    src = 'https://github.com/user/plugin2',
    version = 'main',  -- Branch name, tag, or commit hash
  },

  -- Custom plugin name
  {
    src = 'https://github.com/user/generic-name',
    name = 'custom-name'
  }
})

-- Update all managed plugins
vim.pack.update()

-- Or using lazy.nvim (external plugin manager)
-- ~/.config/nvim/init.lua
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git", "clone", "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable",
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)

require("lazy").setup({
  {
    'neovim/nvim-lspconfig',
    config = function()
      require('lspconfig').lua_ls.setup({})
      require('lspconfig').pyright.setup({})
    end
  },
  {
    'nvim-treesitter/nvim-treesitter',
    build = ':TSUpdate',
    config = function()
      require('nvim-treesitter.configs').setup({
        ensure_installed = { "lua", "python", "javascript" },
        highlight = { enable = true },
      })
    end
  }
})
```

## Summary

Neovim serves as both a powerful terminal-based text editor and a programmable text manipulation engine accessible via multiple interfaces. The primary use cases include: interactive editing with modern IDE features (LSP, diagnostics, autocomplete, inlay hints, inline completion), automation through Lua scripting, remote control via RPC for GUI frontends or external tools, and plugin development extending editor functionality. The built-in LSP client eliminates the need for language-specific plugins, while TreeSitter provides fast syntax highlighting and code analysis. The diagnostic framework standardizes error reporting across linters and language servers. Recent additions include native snippet support via vim.snippet, a built-in package manager (vim.pack), LSP inline completion for Copilot-style AI suggestions, and inlay hints for enhanced code context.

Integration patterns vary based on the use case: embedded instances communicate through stdin/stdout using MessagePack-RPC, GUI clients connect via TCP sockets or Unix domain sockets, remote plugins run as separate processes with bidirectional RPC communication, and Lua scripts execute directly within the editor's runtime. The API maintains backward compatibility through versioning, allowing clients to query supported features. Neovim's event-driven architecture with multiqueue processing ensures UI responsiveness while handling expensive operations, and the separation between fast and deferred API calls prevents blocking on user input. The comprehensive API covering buffers, windows, highlighting, autocommands, snippets, and LSP integration enables building sophisticated text editing applications on top of Neovim's proven foundation. The native package manager (vim.pack) provides a streamlined way to manage plugins with version constraints and automatic updates, while the snippet engine offers TextMate-compatible snippet expansion without external dependencies.
