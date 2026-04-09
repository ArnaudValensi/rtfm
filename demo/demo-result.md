# SDL3 create a window

```
SDL_CreateWindow
  Create a window with a given title, size, and flags.
  SDL_Window * SDL_CreateWindow(const char *title, int w, int h, SDL_WindowFlags flags);
  Returns SDL_Window* or NULL on failure (check SDL_GetError()).
  -> https://wiki.libsdl.org/SDL3/SDL_CreateWindow
```

Note: SDL3 changed the signature from SDL2 — `x`/`y` position params were removed. The window is shown by default; pass `SDL_WINDOW_HIDDEN` to suppress. If using an `SDL_Renderer`, prefer `SDL_CreateWindowAndRenderer()` to avoid flicker.

Common flags: `SDL_WINDOW_RESIZABLE`, `SDL_WINDOW_FULLSCREEN`, `SDL_WINDOW_HIDDEN`, `SDL_WINDOW_OPENGL`, `SDL_WINDOW_VULKAN`, `SDL_WINDOW_METAL`, `SDL_WINDOW_HIGH_PIXEL_DENSITY`.

Sources:
- [SDL3/SDL_CreateWindow - SDL Wiki](https://wiki.libsdl.org/SDL3/SDL_CreateWindow)
- [SDL3/SDL_WindowFlags - SDL Wiki](https://wiki.libsdl.org/SDL3/SDL_WindowFlags)
