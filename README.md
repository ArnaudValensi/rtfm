# rtfm

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
git clone <repo-url> ~/.rtfm && ln -sf ~/.rtfm/rtfm ~/.local/bin/rtfm
```

Requires [Claude Code](https://claude.ai/claude-code) installed and authenticated.

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

## Philosophy

- Official docs first, always
- Verify before answering — unverified info is marked as such
- Stay in the terminal, stay in flow
- Lookup tool, not a coding assistant
