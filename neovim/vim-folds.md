---
title: "Neovim Folds Explained"
created: 2024-03-23
updated: 2025-03-23
tags:
  - neovim
  - vim
  - editor
  - productivity
  - folding
  - treesitter
status: active
---

# Neovim Folds Explained

## Overview
This note explains how to use folds in Neovim to collapse and expand sections of text, improving navigation and management of large files. It covers different fold methods, basic and comprehensive fold commands, and the integration of folds with Treesitter, which is the preferred method for automatic, syntax-aware folding.

## Fold Methods

**Key Concepts:**
- **manual**: Create folds by hand with commands (less preferred for automatic workflows).
- **indent**: Fold based on line indentation.
- **expr**: Use custom expressions to determine folds (often used with Treesitter).
- **marker**: Define folds using special text markers in your file.
- **syntax**: Create folds based on syntax highlighting (less efficient than Treesitter).
- **diff**: Special folding for diff mode.

Neovim supports several ways to define folds. For users who prefer automatic folding based on code structure, **Treesitter (using the `expr` foldmethod)** is the recommended approach. Indentation-based folding (`indent`) is also a common automatic method. Manual fold creation is available but may be less frequently used in workflows prioritizing automation.

You can set the fold method with: `:set foldmethod=expr` (for Treesitter) or `:set foldmethod=indent` (for indentation-based folding).

## Basic Fold Commands

| Command     | Action                            | Usefulness |
| ----------- | --------------------------------- | ---------- |
| `zf{motion}`| Create a fold (manual mode)       | ★★☆☆☆    |
| `zo`        | Open a fold under cursor          | ★★★★★    |
| `zc`        | Close a fold under cursor         | ★★★★★    |
| `za`        | Toggle fold under cursor          | ★★★★★    |
| `zR`        | Open all folds                    | ★★★★☆     |
| `zM`        | Close all folds                   | ★★★★☆     |
| `zj`/`zk`   | Move to next/previous fold       | ★★★★☆     |
| `zd`        | Delete fold under cursor (manual) | ★☆☆☆☆    |

## Comprehensive Neovim Fold Commands

This section provides a complete reference of fold commands in Neovim with explanations and usefulness ratings based on general usage. For workflows primarily utilizing Treesitter or indentation-based folding, the open/close commands (`zo`, `zc`, `za`, `zO`, `zC`, `zA`, `zR`, `zM`) and navigation commands (`zj`, `zk`) will likely be the most frequently used.

**Usefulness Rating:** The rating reflects the general utility of the command in various Neovim workflows. Commands highly relevant for automatic folding methods are marked accordingly.

### Basic Fold Operations

|Command|Description|Usefulness|Notes|
|---|---|---|---|
|`zo`|Open fold under cursor|★★★★★|Essential for viewing folded content.|
|`zc`|Close fold under cursor|★★★★★|Essential for hiding content.|
|`za`|Toggle fold under cursor|★★★★★|Most frequently used command.|
|`zO`|Open fold recursively|★★★★☆|Very useful for deep nesting.|
|`zC`|Close fold recursively|★★★★☆|Very useful for cleaning up view.|
|`zA`|Toggle fold recursively|★★★★☆|Versatile for deep structures.|

### Creating Folds (Manual Mode)

|Command|Description|Usefulness|Notes|
|---|---|---|---|
|`zf{motion}`|Create fold over motion|★★★☆☆|Useful in manual mode.|
|`{visual}zf`|Create fold over selection|★★★☆☆|Convenient for manual folding.|
|`:{range}fo[ld]`|Create fold for lines in range|★★☆☆☆|Less common but handy.|
|`zF`|Create fold for N lines|★★☆☆☆|Situational.|

### Navigating Folds

|Command|Description|Usefulness|Notes|
|---|---|---|---|
|`zj`|Move to next fold|★★★★☆|Great for navigation.|
|`zk`|Move to previous fold|★★★★☆|Great for navigation.|
|`[z`|Move to start of current fold|★★★☆☆|Useful for editing.|
|`]z`|Move to end of current fold|★★★☆☆|Useful for editing.|

### Opening/Closing Multiple Folds

|Command|Description|Usefulness|Notes|
|---|---|---|---|
|`zR`|Open all folds|★★★★★|Essential when needing full view.|
|`zM`|Close all folds|★★★★★|Essential for overview.|
|`zm`|Fold more (decrease foldlevel)|★★★☆☆|Good for incremental focusing.|
|`zr`|Fold less (increase foldlevel)|★★★☆☆|Good for incremental expanding.|
|`zn`|Disable folding|★★☆☆☆|Situational.|
|`zN`|Re-enable folding|★★☆☆☆|Situational.|
|`zi`|Toggle folding entirely|★★★☆☆|Quick way to switch modes.|

### Other Fold Operations

|Command|Description|Usefulness|Notes|
|---|---|---|---|
|`zd`|Delete fold under cursor|★★☆☆☆|Only for manual folds.|
|`zD`|Delete fold recursively|★★☆☆☆|Only for manual folds.|
|`zE`|Eliminate all folds|★★☆☆☆|Only for manual folds.|
|`zx`|Update folds and apply foldlevel|★★★☆☆|Useful when changing fold method.|
|`zX`|Update folds, set foldlevel=0|★★☆☆☆|Specialized use.|
|`zv`|Open just enough folds to see cursor|★★★★★|Very useful after searches.|
|`zH`|Scroll half-screen to the right|★☆☆☆☆|Rarely needed.|
|`zL`|Scroll half-screen to the left|★☆☆☆☆|Rarely needed.|

### Fold Settings (Command Mode)

|Setting|Description|Usefulness|Notes|
|---|---|---|---|
|`:set foldmethod=`|Set folding method (manual, indent, expr, marker, syntax, diff)|★★★★★|Essential configuration. Use `expr` for Treesitter or `indent` for indentation.|
|`:set foldlevel=N`|Set fold level (0=all closed, higher=more open)|★★★★★|Critical for controlling view.|
|`:set foldcolumn=N`|Show fold indicators in sidebar (N columns wide)|★★★☆☆|Helpful visual aid.|
|`:set foldminlines=N`|Minimum lines for a fold to be closed|★★☆☆☆|Occasional fine-tuning.|
|`:set foldnestmax=N`|Maximum nesting level for folds|★★☆☆☆|Occasional fine-tuning.|

## Advanced Fold Tips

- The most commonly used commands in daily work, especially with automatic folding, are `za`, `zR`, `zM` and `zj`/`zk`.
- With Treesitter, you'll primarily interact with folds using the open/close commands rather than manual creation. The structure of folds is determined by the syntax tree.
- For programming, the combination of `zc` (close) and `zv` (view cursor) helps maintain focus while navigating code.

Would you like more details on any specific commands or how to create custom fold mappings?

# Treesitter and Neovim Folds

Treesitter integration significantly enhances folding in Neovim by making it syntax-aware. This is the preferred method for many users as it provides intelligent and automatic folding based on the code structure.

## Treesitter Folding Setup

To use Treesitter for folding:

```vim
" Enable treesitter folding
set foldmethod=expr
set foldexpr=nvim_treesitter#foldexpr()
```

Or in Lua (init.lua):

```lua
vim.opt.foldmethod = "expr"
vim.opt.foldexpr = "nvim_treesitter#foldexpr()"
```

**Example:** After setting up Treesitter folding, Neovim will automatically create folds for functions, classes, loops, and other code blocks based on the syntax of the programming language. You can then use `zo` to open a specific function's body or `zc` to close it.

## Advantages Over Traditional Folding

1.  **Syntax-Aware Folding**: Folds match actual code structures (functions, classes, blocks) rather than just indentation levels. This provides more accurate and meaningful folding.
2.  **Language-Specific Understanding**: Treesitter understands different programming languages and folds appropriately for each, respecting the language's syntax rules.
3.  **Nested Code Blocks**: Properly handles nested blocks, conditionals, and loops as discrete foldable units, allowing for precise control over the level of detail you see.
4.  **Performance**: Generally more efficient than syntax-based folding for large files as it relies on a parsed syntax tree.

## Code Block Folding Examples

With Treesitter, you get intelligent folding of:
- Function and method bodies
- Class definitions
- Control structures (if/else, loops, etc.)
- Try/catch blocks
- Import/require sections

**Example:** In a Python file, a `def my_function():` block will automatically become foldable. In a JavaScript file, a `function myFunction() { ... }` block will be foldable.

## Configuration Options

You can customize Treesitter folding behavior:

```lua
require('nvim-treesitter.configs').setup {
  fold = {
    enable = true,
  },
}

-- Set initial fold level (optional - 99 means all folds are initially open)
vim.opt.foldlevel = 99
```

**Example:** Setting `foldlevel = 0` would start with all Treesitter-defined folds closed.
