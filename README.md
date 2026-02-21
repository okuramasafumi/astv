# Ruby AST Tree Viewer — Spec

[visit Viewer](https://ko1.github.io/astv/)

## Purpose
Visualize Ruby ASTs (Prism or parse.y) as a compact tree and compare them with a traditional text representation.

## Inputs
- Ruby source (parsed in the browser via Ruby.wasm + Prism/parse.y)

## Initial Load Behavior
- If URL has `?p=...`, its value is inserted into the Ruby editor.
- Otherwise the sample Ruby code is used.
- Rendering is triggered manually (Render button or shortcut).

## Core Behavior
- Ruby input -> AST (Prism or parse.y) -> JSON -> Tree/JSON
- Text tab shows `inspect` output of the AST root (Prism) or parse.y dump (parse.y)
- Tree tab shows a compact node graph
- JSON tab shows formatted JSON

## Node Rules
- A node is an object that has a `type` key.
- An array becomes child nodes only if **all** elements are node objects.
- Empty arrays are treated as additional info (not child nodes).
- Any object **without** `type` is treated as additional info.
- `location` is additional info.
- `locals` is additional info.

## Representative Value
- A node displays: CapitalCase version of `type` as the representative value.
- Priority order: `name` > `value` > `unescaped`.
- If the node has `name`, show: `Type (name)`.
- If the node has numeric `value`, show: `Type (value: N)`.
- If the node has `unescaped`, show: `Type (unescaped: "...")`.

## Relations
- Relation labels are shown outside the node box.
- For array relations, show size: `relation (size: N)`.

## Details / Expansion
- Additional info is stored as details and can be expanded by clicking the node.
- Click again to collapse.
- While selecting text, clicking does not toggle expansion.
- Expand All / Collapse All buttons control every node.

## Tree Folding
- Nodes with child subtrees display a fold toggle (▶/▼).
- Clicking the fold toggle hides or shows the entire subtree beneath the node.
- Fold All / Unfold All buttons fold or unfold every node with children.

## Text vs Tree
- Output pane is tabbed: Tree / Text / JSON.
- Text and JSON tabs include a Copy button.

## Ruby Editor
- Simple syntax highlight (overlay + highlight.js).
- Ctrl/Cmd+Enter triggers Render.
- A node with `location` highlights the corresponding Ruby source range on hover (1-based columns).

## URL Share
- `?p=...` populates the Ruby editor.
- `Copy URL` builds a shareable URL with current editor content.

## UI Layout
- Left: Ruby input
- Right: Tree/Text/JSON output
- AST mode selector: Prism AST / parse.y AST
- Footer shows Ruby.wasm load status and version

## Security Notes
- Tree rendering uses DOM APIs (`textContent`) to reduce XSS risk.
- Ruby.wasm executes user-provided code; heavy input can freeze the page.

## Credits
- Built with assistance from Codex.

## Copyright
Copyright (c) 2026 Koichi Sasada

Repository:
```
https://github.com/ko1/astv
```
