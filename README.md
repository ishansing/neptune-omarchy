# Neptune Dark

Dark Omarchy theme. Custom variant of `neptune`.

## Files

- `colors.toml` — theme colors
- `icons.theme` — icon set
- `backgrounds/` — wallpapers

## Notes

- `colors.toml` defines `selection_foreground = "#05060d"` so selected text is
  dark on the light-blue selection instead of white.
- **Neovim caveat:** aether.nvim (the colorscheme this theme uses) never
  applies `selection_foreground` to its `Visual` highlight — it only sets a
  background, so selected text falls back to the light foreground and becomes
  invisible. Fix requires the plugin file
  [`~/.config/nvim/lua/plugins/visual-selection.lua`](file:///home/zeref/.config/nvim/lua/plugins/visual-selection.lua),
  which overrides `Visual`/`VisualNOS` via aether's `on_highlights` hook:

  ```lua
  return {
    {
      "aether",
      opts = {
        on_highlights = function(highlights, colors)
          highlights.Visual = { fg = colors.background, bg = colors.selection }
          highlights.VisualNOS = { fg = colors.background, bg = colors.selection }
        end,
      },
    },
  }
  ```

  Without it, selected text in nvim is invisible. This file lives outside the
  theme dir because themes can't ship `.lua` that nvim loads.