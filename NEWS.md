# What's new?

## 11.x

- new option `vim.g.deprecation_warnings` to disable deprecation warnings
  Defaults to `false`. To disable, set it to `true` in your `options.lua`

- `vim-illuminate` move to extras
  Document highlights now use native lsp functionality by default

Since Neovim 0.10 has been released, I've been working on a new version of **LazyVim**
that is fully compatible with all the latest Neovim features.

Additionally, some core plugins have been moved to extras.

- `native snippets` are now the default on Neovim 0.10
  Older versions of Neovim will use the new `luasnip` extra.

- `native comments` are now the default on Neovim 0.10
  Older versions of Neovim will use the new `mini-comment` extra.
  `nvim-ts-context-commentstring` has been integrated in the native comments.

- `inlay hints` have been in **LazyVim** for a while, but are now
  enabled by default. To disable them:

  ```lua
  {
    "nvim-lspconfig",
    opts = {
      inlay_hints = { enabled = false },
    }
  }
  ```

- plugins moved to extras:

  - `mini.ai` which I couldn't live without, but not everyone needs it
  - `mini.surround`
  - `mini.indentscope` scopes are now also highlighted with `indent-blankline`
  - `nvim-treesitter-context`

- There's a new extra for the `nvim-treesitter` **rewrite**.
  Since the rewrite is not backward compatible, some plugins will be disabled
  when you enable this extra: `vim-illuminate`, `nvim-ts-autotag`, and `nvim-ts-autotag`.
  I would **NOT** recommend enabling this extra for now.

## 10.x

- added new extra for [mini.diff](https://github.com/echasnovski/mini.nvim/blob/main/readmes/mini-diff.md)
  This is a plugin similar to gitsigns but with a neat diff overlay
  that can be toggled with `<leader>go`.

- **trouble.nvim** has been rewritten from scratch and is now in beta.
  I've added a new extra for it (`trouble-v3`) for those of you who want to try it out.
  You can find the updated docs [here](https://github.com/folke/trouble.nvim/tree/dev)

- The **lazygit** integration now configures:

  - the theme based on the colorscheme
  - nerd font icons (v3)
  - editor preset is set to `nvim-remote` for better interop with Neovim

- The option `vim.g.lazygit_theme` was renamed to `vim.g.lazygit_config`

- **lazygit** now automatically uses the colors of your current colorscheme.
  This is enabled by default. To disable, add the below to your `options.lua`:

  ```lua
  vim.g.lazygit_config = false
  ```

- Added support for `basedpyright` to the **python** extra.
  Enable in your `options.lua` with:

  ```lua
  vim.g.lazyvim_python_lsp = "basedpyright"
  ```

  Be aware that `basedpyright` is still in development and
  may not work exactly the same as `pyright`.

- User extras under `lua/plugins/extras` can now also be managed
  with **LazyExtras**

- `nvim-ts-autotag` is now included by default

- `nvim-treesitter-context` is now included by default

- Added extra for `symbols-outline.nvim`

- Added extra for `aerial.nvim`

- `nvim-navic` has been removed. If you want to keep using `nvim-navic`,
  you can enable the **editor.navic** extra

- New `:LazyExtras` command for managing **LazyVim** extras

- Improved **formatting**:

  - **LazyVim** can now work with multiple formatters. Types:

    - **primary**: only one primary formatter can be active at a time.
      _(conform, none-ls, LSP)_
    - **secondary**: multiple secondary formatters can be active _(eslint, ...)_

  - **LazyVim** automatically selects the primary formatter based on the
    current available sources and priorities.

  - New `:LazyFormat` command for formatting the current selection or buffer
  - New `:LazyFormatInfo` command for displaying the active formatters
    for the current buffer
  - Auto-formatting can be disabled with:

    ```lua
    vim.g.autoformat = false -- globally
    vim.b.autoformat = false -- buffer-local
    ```

- `none-ls.nvim` is no longer installed by default

  - `conform.nvim` is now the default formatter
  - `nvim-lint` is now the default linter
  - If you want to keep using `none-ls.nvim`,
    you can enable the **lsp.none-ls** extra

- `dashboard.nvim` is the new default dashboard plugin

  - If you want to keep using `alpha.nvim`, you can enable the **ui.alpha** extra

- Improved **root detection**:

  - New `:LazyRoot` command that shows info about the root dir detection
  - Configurable with `vim.g.root_spec`

    ```lua
    -- LazyVim root dir detection
    -- Each entry can be:
    -- * the name of a detector function like `lsp` or `cwd`
    -- * a pattern or array of patterns like `.git` or `lua`.
    -- * a function with signature `function(buf) -> string|string[]`
    vim.g.root_spec = { "lsp", { ".git", "lua" }, "cwd" }

    -- To disable root detection set to just "cwd"
    vim.g.root_spec = { "cwd" }
    ```
