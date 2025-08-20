# bwzy - bitwarden ... fuzzy

bwzy is a fuzzy finder for Bitwarden using the official bitwarden cli.

The `bw` cli is great, but not very user-friendly.

`bwzy` tries to make this quicker by caching the information and presenting it via the magnificient [fzf](https://junegunn.github.io/fzf/).

# current features
- READ-ONLY ui
- search based on name and folder
- copy user/pass/totp
- cache the items in shared memory (`/dev/shm/`) to make it fast
- cache does not persist through reboots (by default)
- refresh/flush cache
- preview items in `YAML` form
- auto-fill for hyprland

# requirements

The following software is needed by `bwzy`:

- [fzf](https://junegunn.github.io/fzf/) for fuzzy finding
- [bitwarden cli client](https://contributing.bitwarden.com/getting-started/clients/cli) to access bitwarden
- [jq](https://jqlang.github.io/jq/) to work with the JSON
- [OATH Toolkit](https://www.nongnu.org/oath-toolkit/) allows generating TOTP tokens
- [charmbracelet - gum](https://github.com/charmbracelet/gum) for the loading spinner and color

it also expects `grep`, `sed` and `awk` to be available

Additinally, you will need clipboard and keyboard automation such as `wtype` and `wl-copy` under wayland.

## configuration

All configuration is done via environment variables, with defaults shown

```bash
BWZY_CACHE=`/dev/shm/bwzy-cache` # where the passwords are cached
BWZY_KEEP_CACHE='true'           # set to false and cache will be purged
BWZY_COPY_CMD='wl-copy'          # the command to copy something to the clipboard
BWZY_TYPE_CMD='wtype'            # the command used to type / send keyboard events
BWZY_HIDE_CMD=''                 # the command to hide bwzy
BWZY_REFOCUS_CMD=''              # the command to refocuse the previous window
BWZY_COPY_AND_HIDE='true'        # set to 'false' to not hide bwzy on copy
BWZY_NOTIFY_CMD='notify-send -i bitwarden' # send a notification
# cosmetic overrides which adjust the looks
BWZY_USER_SYMBOL='u+'
BWZY_PASS_SYMBOL='p+'
BWZY_TOTP_SYMBOL='t+'
BWZY_LINK_SYMBOL='l+'
BWZY_AUTO_SYMBOL='a+'
BWZY_FOLDER_SYMBOL='/'
BWZY_POINTER_SYMBOL='> '
BWZY_PROMPT_SYMBOL='? '
```

Note: under [hyprland](https://hypr.land/) the following works:
```bash
BWZY_HIDE_CMD=hyprctl dispatch movetoworkspacesilent special:tools,title:bwzy
BWZY_REFOCUS_CMD=hyprctl dispatch focuscurrentorlast
```
which places the bwzy window launched vi the [bwzy.desktop](./bwzy.desktop) file into a special workspace when not needed.

```bash
BWZY_USER_SYMBOL=' '
BWZY_PASS_SYMBOL=' '
BWZY_AUTO_SYMBOL=' '
BWZY_TOTP_SYMBOL=' '
BWZY_LINK_SYMBOL=' '
BWZY_FOLDER_SYMBOL='/'
BWZY_POINTER_SYMBOL=' '
BWZY_PROMPT_SYMBOL=' '
```

## arch install
```bash
pacman -S fzf bitwarden-cli jq haskell-yaml oath-toolkit gum
```
## install dependency


Arch Linux:
```bash
sudo pacman -S --needed wtype ydotool xdotool xvkbd wl-clipboard xclip xsel bat jq sed awk fzf
```
## tips and tricks

By default the cache is removed on reboot since it lives in `/dev/shm/`. if you have a secure encrypted file system you can override the cache location so that it persists during reboots. Be safe and know your risks. 

# feature ideas
- ~~auto-fill~~ (done)
- ~~"archive" feature to filter thingsi~~ (done)
- ability to edit an entry
- ability to add a new entry
