# bwzy - bitwarden ... fuzzy

bwzy is a fuzzy finder for Bitwarden using the official bitwarden cli.

The `bw` cli is great, but not very user-friendly.

`bwzy` tries to make this quicker by caching the information and presenting it via the magnificient [fzf](https://junegunn.github.io/fzf/).

# current features
- search based on name and folder
- copy user/pass/totp
- cache the items in shared memory (`/dev/shm/`) to make it fast
- cache does not persisted through reboots
- refresh cache
- preview items in `YAML` form

# requirements

The following software is needed by `bwzy`:

- [fzf](https://junegunn.github.io/fzf/) for fuzzy finding
- [bitwarden cli client](https://contributing.bitwarden.com/getting-started/clients/cli) to access bitwarden
- [jq](https://jqlang.github.io/jq/) to work with the JSON
- [OATH Toolkit](https://www.nongnu.org/oath-toolkit/) allows generating TOTP tokens
- [charmbracelet - gum](https://github.com/charmbracelet/gum) for the loading spinner and color

it also expects `sed` and `awk` to be available

## arch install
```bash
pacman -S fzf bitwarden-cli jq haskell-yaml oath-toolkit gum
```

# feature ideas
- auto-fill
- "archive" feature to filter things
- ability to edit an entry
- ability to add a new e.ntry
