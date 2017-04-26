# vim-easyescape

```
_____                  _____                          
 | ____|__ _ ___ _   _  | ____|___  ___ __ _ _ __   ___ 
 |  _| / _` / __| | | | |  _| / __|/ __/ _` | '_ \ / _ \
 | |__| (_| \__ \ |_| | | |___\__ \ (_| (_| | |_) |  __/
 |_____\__,_|___/\__, | |_____|___/\___\__,_| .__/ \___|
                 |___/                      |_|
```

Pull out your Escape key!

`<ESC>/<C-[>/<C-C>` is hard to press?  Try `vim-easyescape`! `vim-easyescape` makes exiting insert mode easy and distraction free.

## Problems
Traditionally, we need to use
```
inoremap jk <Esc>
inoremap kj <Esc>
```
or
```
inoremap jj <Esc>
```
so that we can press `jk` simultaneously (in arbitrary order since we have two maps) or press `j` twice to exit the insert mode.  However, a problem with such map sequence is that Vim will pause whenever you type `j` or `k` in insert mode (it is waiting for the next key to determine whether to apply the mapping). The pause causes visual distraction which you may or may not notice.

`vim-easyescape` does not have such problem and supports custom timeout.

## Installation
Use your favourite plugin manager, e.g., `vim-plug`:
```
Plug "zhou13/vim-easyescape"
```

## Usage

### Configuration 1: map of `jk` and `kj` (recommended)

The unit of timeout is in ms.  A very small timeout makes an input of real `jk` or `kj` possible (Python3 is required for this feature)!
```
let g:easyescape_chars = { "j": 1, "k": 1 }
let g:easyescape_timeout = 100
cnoremap jk <ESC>
cnoremap kj <ESC>
```

### Configuration 2: map of `jj`

```
let g:easyescape_chars = { "j": 2 }
let g:easyescape_timeout = 100
cnoremap jj <ESC>
```

## Dependency

Python3 is required if timeout (`g:easyescape_timeout`) is less than 2000 ms because vim does not provide a way to fetch sub-second time.

## Known problems

1. Maps of keys in `g:easyescape_chars` need to be created.
2. Does not work in command/visual mode due to lack of `InsertCharPre` in vim/nvim.
