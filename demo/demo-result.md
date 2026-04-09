```
SDL_CreateWindow
  Create a window with the specified title, dimensions, and flags.
  SDL_Window * SDL_CreateWindow(const char *title, int w, int h, SDL_WindowFlags flags);
  -> https://wiki.libsdl.org/SDL3/SDL_CreateWindow
```

**Parameters:**
- `title` — window title (UTF-8)
- `w`, `h` — width and height in pixels
- `flags` — 0 or OR'd `SDL_WindowFlags` (e.g. `SDL_WINDOW_OPENGL`, `SDL_WINDOW_RESIZABLE`, `SDL_WINDOW_HIDDEN`)

**Returns:** `SDL_Window *` on success, `NULL` on failure (check `SDL_GetError()`).

```c
SDL_Window *window = SDL_CreateWindow("My App", 800, 600, SDL_WINDOW_RESIZABLE);
if (!window) {
    SDL_Log("Failed: %s", SDL_GetError());
}
```

Note: SDL3 removed the `x, y` position parameters that SDL2 had. Use `SDL_SetWindowPosition()` after creation if needed. Window is shown by default unless `SDL_WINDOW_HIDDEN` is set.
