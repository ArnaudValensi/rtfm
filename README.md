```
┬─┐┌┬┐┌─┐┌┬┐
├┬┘ │ ├┤ │││
┴└─ ┴ └  ┴ ┴
```

API documentation lookup in your terminal. Powered by Claude Code.

Like `tldr` or `cheat.sh`, but for any programming API — backed by real doc verification, not static cheat sheets.

```
$ rtfm "SDL3 configure OpenGL context attributes"

SDL_GL_SetAttribute
  Set an OpenGL context attribute. Call BEFORE creating the window.
  bool SDL_GL_SetAttribute(SDL_GLAttr attr, int value);
  -> https://wiki.libsdl.org/SDL3/SDL_GL_SetAttribute
```

## Install

```sh
git clone https://github.com/ArnaudValensi/rtfm.git ~/.rtfm && ln -sf ~/.rtfm/rtfm ~/.local/bin/rtfm
```

### Dependencies

- [Claude Code](https://claude.ai/claude-code) — required
- [glow](https://github.com/charmbracelet/glow) — Markdown rendering (skip with `-r`)
- [fzf](https://github.com/junegunn/fzf) — history search (`-f`, `-F`)
- [ripgrep](https://github.com/BurntSushi/ripgrep) — content search (`-F`)

```sh
# Arch
pacman -S glow fzf ripgrep

# macOS
brew install glow fzf ripgrep
```

## Usage

```
rtfm "your question about an API"
```

### Flags

| Flag | Effect |
|---|---|
| `-s` | Use Sonnet (default: Opus) |
| `-l` | Low effort |
| `-m` | Medium effort |
| `-h` | High effort (default) |
| `-r` | Raw output (no glow rendering) |
| `-f` | Search history by query (fzf) |
| `-F` | Search history by content (rg + fzf) |
| `--help` | Show help |

Flags combine: `-sl` = Sonnet + low, `-sm` = Sonnet + medium.

### Examples

```sh
rtfm "SDL3 configure OpenGL context"
rtfm "OpenGL set depth buffer bits"
rtfm "posix shared memory"
rtfm -sm "linux epoll usage"
rtfm -s "vulkan create swap chain"
```

## How it works

1. Claude identifies candidate functions from your question
2. Searches the web for official documentation
3. Fetches the actual doc page to verify
4. Prints a concise, verified result with doc links

It also has read-only access to your codebase to detect which library versions you use.

## NeoVim Integration

Add this to your keymaps or `init.lua` to use `:Rtfm` as a command inside NeoVim. It opens a horizontal split with the result. Press `q` to close when done.

```lua
vim.api.nvim_create_user_command("Rtfm", function(opts)
  vim.cmd("split")
  vim.cmd("terminal rtfm " .. opts.args)
  vim.cmd("startinsert")
  vim.api.nvim_create_autocmd("TermClose", {
    buffer = 0,
    once = true,
    callback = function()
      vim.bo.bufhidden = "wipe"
      vim.keymap.set("n", "q", "<cmd>close<cr>", { buffer = true })
    end,
  })
end, { nargs = "+", desc = "rtfm — API doc lookup" })
```

Usage inside NeoVim:

```
:Rtfm SDL3 create window
:Rtfm -sm OpenGL depth buffer bits
```

## Philosophy

- Official docs first, always
- Verify before answering — unverified info is marked as such
- Stay in the terminal, stay in flow
- Lookup tool, not a coding assistant
