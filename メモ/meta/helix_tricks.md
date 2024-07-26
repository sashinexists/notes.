# Helix tricks
// maybe come up with a better name for this document
- You can press `shift+a` to move the cursor to the end of a line and switch to insert mode
  - or `shift+i` to move it to the beginning and switch to insert mode (this takes it to the first non-whitespace character)
- `g s` moves the cursor to the first non-whitespace character in a line *without* also switching to insert mode
- `m s` to surround a selection with something
  - eg; `m s (` to surround a selection with brackets or `m s "` to surround a selection with quotes
