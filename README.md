# Herdr Copy Reference

Right-click a **tab** or a **terminal pane** in Herdr → **Copy reference**. The clipboard gets one line whose first token is the `hc` address another agent can act on:

```text
t9 — herdr · opencode working · "OC | Terminal tab IDs for agent sync" · tab "OpenCode" (tb…) · space "~" (sp…) · /Users/pablowerlang · hc: get/read/send/wait t9
```

Then, from another terminal or agent:

```sh
hc get t9
hc read t9 --lines 80
hc send t9 "…"
hc wait t9
```

On another machine the first token is `machine/t9`.

## Requirements

- Herdr app (the mods are app mods, not TUI plugins).
- macOS, Linux, or Windows for the clipboard write.
- Linux clipboard needs `wl-copy` (Wayland) or `xclip` (X11).

## Install

This is a two-mod feature:

- `mods/ref-menu` — clone of the shipped `menu` with the copy item.
- `mods/tabs-ref` — clone of the shipped `tabs` that opens `ref-menu` for tab right-clicks.

Copy/sync both into `~/.config/herdr-app/mods/`, then wire a **personal layout**:

```json
{
  "terminal_menu": "ref-menu",
  "children": [
    {
      "id": "tabs",
      "type": "block",
      "content": { "mod": "tabs-ref" }
    }
  ]
}
```

The shipped `main`, `tabs`, and `menu` must stay untouched. Clone the layout first if needed:

```sh
herdr-app do layout.clone --name main --as my-layout
```

After wiring, run:

```sh
herdr-app check ~/.config/herdr-app/mods/ref-menu
herdr-app check ~/.config/herdr-app/mods/tabs-ref
```

## How it works

- `mods/ref-menu` is a clone of Herdr's `menu`; `ref.js` builds the reference line and `copy.svg` is the menu icon.
- `mods/tabs-ref` is a clone of `tabs`; it opens `ref-menu` on tab right-click and sizes the popup to its rows.
- The layout root's `terminal_menu` routes pane right-clicks to `ref-menu` too.
- On a TUI that captures the mouse, use **Shift+right-click** to open Herdr's menu.
- `herdr-app do mod.open --name ref-menu` opens the current tab's references without right-clicking.

## Repository

Source of truth for both mods. After edits:

```sh
./sync.sh
```

The script syncs both mods to the live Herdr folder and runs `herdr-app check`. See `AGENTS.md`.

## Publish

This repo is an app-mod repo. To share it on `herdr.dev/mods`:

- keep `mods/ref-menu` and `mods/tabs-ref` at the root;
- keep `RECIPE.md` and `preview.png`;
- add the topic `herdr-mod`;
- make the repository public.

See `.agents/skills/herdr-publish/SKILL.md` and `references/publishing.md` for the full checklist.
