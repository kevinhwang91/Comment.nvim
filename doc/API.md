# ⚙️ API

Following are list of APIs that are exported from the plugin. These can be used to setup [custom keybinding](#usage) or to make your own custom comment function. All API functions can take a `{motion}` (Read `:h :map-operator`) and a optional [`{cfg}`](../README.md#config) argument which can be used to override the [default configuration](../README.md#config)

<details>
<summary>Deprecated API</summary>

```lua
---@alias OpMode 'line'|'char'|'v'|'V' Vim operator-mode motions. Read `:h map-operator`
```

### Core

These APIs powers the [basic-mappings](../README.md#basic-mappings).

```lua
--######### LINEWISE #########--

---Toggle linewise-comment on the current line
---@param cfg? CommentConfig
require('Comment.api').toggle_current_linewise(cfg)

---(Operator-Pending) Toggle linewise-comment on the current line
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').toggle_current_linewise_op(opmode, cfg)

---(Operator-Pending) Toggle linewise-comment over multiple lines
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').toggle_linewise_op(opmode, cfg)

---Toggle linewise-comment over multiple lines using `vim.v.count`
---@param cfg? CommentConfig
require('Comment.api').toggle_linewise_count(cfg)

--######### BLOCKWISE #########--

---Toggle blockwise comment on the current line
---@param cfg? CommentConfig
require('Comment.api').toggle_current_blockwise(cfg)

---(Operator-Pending) Toggle blockwise comment on the current line
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').toggle_current_blockwise_op(opmode, cfg)

---(Operator-Pending) Toggle blockwise-comment over multiple lines
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').toggle_blockwise_op(opmode, cfg)

---Toggle blockwise-comment over multiple lines using `vim.v.count`
---@param cfg? CommentConfig
require('Comment.api').toggle_blockwise_count(cfg)
```

### Extra

These APIs powers the [extra-mappings](../README.md#extra-mappings) and also provides the blockwise version.

```lua
--######### LINEWISE #########--

---Insert a linewise-comment below
---@param cfg? CommentConfig
require('Comment.api').insert_linewise_below(cfg)

---Insert a linewise-comment above
---@param cfg? CommentConfig
require('Comment.api').insert_linewise_above(cfg)

---Insert a linewise-comment at the end-of-line
---@param cfg? CommentConfig
require('Comment.api').insert_linewise_eol(cfg)

--######### BLOCKWISE #########--

---Insert a blockwise-comment below
---@param cfg? CommentConfig
require('Comment.api').insert_blockwise_below(cfg)

---Insert a blockwise-comment above
---@param cfg? CommentConfig
require('Comment.api').insert_blockwise_above(cfg)

---Insert a blockwise-comment at the end-of-line
---@param cfg? CommentConfig
require('Comment.api').insert_blockwise_eol(cfg)
```

### Extended

These APIs powers the [extended-mappings](../README.md#extended-mappings).

```lua
--######### LINEWISE #########--

---Comment current line using linewise-comment
---@param cfg? CommentConfig
require('Comment.api').comment_current_linewise(cfg)

---(Operator-Pending) Comment current line using linewise-comment
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').comment_current_linewise_op(opmode, cfg)

---(Operator-Pending) Comment multiple line using linewise-comment
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').comment_linewise_op(opmode, cfg)

---Uncomment current line using linewise-comment
---@param cfg? CommentConfig
require('Comment.api').uncomment_current_linewise(cfg)

---(Operator-Pending) Uncomment current line using linewise-comment
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').uncomment_current_linewise_op(opmode, cfg)

---(Operator-Pending) Uncomment multiple line using linewise-comment
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').uncomment_linewise_op(opmode, cfg)

--######### BLOCKWISE #########--

---Comment current line using linewise-comment
---@param cfg? CommentConfig
require('Comment.api').comment_current_blockwise(cfg)

---(Operator-Pending) Comment current line using blockwise-comment
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').comment_current_blockwise_op(opmode, cfg)

---Uncomment current line using blockwise-comment
---@param cfg? CommentConfig
require('Comment.api').uncomment_current_blockwise(cfg)

---(Operator-Pending) Uncomment current line using blockwise-comment
---@param opmode OpMode
---@param cfg? CommentConfig
require('Comment.api').uncomment_current_blockwise_op(opmode, cfg)
```

</details>

### Core

> **NOTE**:
>
> 1. All API functions are dot-repeatable except `*.count()`
> 2. For the `*.current()` functions, `{motion}` argument is optional
> 3. `{cfg}` is optional for all the API functions

```lua
require('Comment.api').toggle.linewise(motion, cfg)
require('Comment.api').toggle.linewise.current(motion, cfg)
require('Comment.api').toggle.linewise.count(count, cfg)

require('Comment.api').toggle.blockwise(motion, cfg)
require('Comment.api').toggle.blockwise.current(motion, cfg)
require('Comment.api').toggle.blockwise.count(count, cfg)

require('Comment.api').comment.linewise(motion, cfg)
require('Comment.api').comment.linewise.current(motion, cfg)
require('Comment.api').comment.linewise.count(count, cfg)

require('Comment.api').comment.blockwise(motion, cfg)
require('Comment.api').comment.blockwise.current(motion, cfg)
require('Comment.api').comment.blockwise.count(count, cfg)

require('Comment.api').uncomment.linewise(motion, cfg)
require('Comment.api').uncomment.linewise.current(motion, cfg)
require('Comment.api').uncomment.linewise.count(count, cfg)

require('Comment.api').uncomment.blockwise(motion, cfg)
require('Comment.api').uncomment.blockwise.current(motion, cfg)
require('Comment.api').uncomment.blockwise.count(count, cfg)
```

### Additional

```lua
---Callback function to provide dot-repeat support
---NOTE: VISUAL mode mapping doesn't support dot-repeat
---@param cb string Name of the API function to call
require('Comment.api').call(cb)
```

<a id="usage"></a>

# ⚙️ Usage

Following are some example keybindings using the APIs.

```lua
-- # NORMAL mode

-- Linewise toggle current line using C-/
vim.keymap.set('n', '<C-_>', '<CMD>lua require("Comment.api").toggle.linewise.current()<CR>')
-- or with dot-repeat support
-- vim.keymap.set('n', '<C-_>', '<CMD>lua require("Comment.api").call("toggle.linewise.current")<CR>g@$')

-- Blockwise toggle current line using C-\
vim.keymap.set('n', '<C-\\>', '<CMD>lua require("Comment.api").toggle.blockwise.current()<CR>')
-- or with dot-repeat support
-- vim.keymap.set('n', '<C-\\>', '<CMD>lua require("Comment.api").call("toggle.blockwise.current")<CR>g@$')

-- Linewise toggle multiple line using <leader>gc with dot-repeat support
-- Example: <leader>gc3j will comment 4 lines
vim.keymap.set('n', '<leader>gc', '<CMD>lua require("Comment.api").call("toggle.linewise")<CR>g@')

-- Blockwise toggle multiple line using <leader>gc with dot-repeat support
-- Example: <leader>gb3j will comment 4 lines
vim.keymap.set('n', '<leader>gb', '<CMD>lua require("Comment.api").call("toggle.blockwise")<CR>g@')

-- # VISUAL mode

-- Linewise toggle using C-/
vim.keymap.set('x', '<C-_>', '<ESC><CMD>lua require("Comment.api").toggle.linewise(vim.fn.visualmode())<CR>')

-- Blockwise toggle using <leader>gb
vim.keymap.set('x', '<leader>gb', '<ESC><CMD>lua require("Comment.api").toggle.blockwise(vim.fn.visualmode())<CR>')
```
