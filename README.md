gvim-open-kindness — Kindly file opener that positions your cursor 🐬
=====================================================================

## SYNOPSIS

`gvim-open-kindness` &lt;servername&gt; &lt;line&gt; &lt;column&gt; &lt;path&gt;...

*(Now with Neovim support! —2025-01-25):*

`nvim-open-kindness` &lt;socketname&gt; &lt;line&gt; &lt;column&gt; &lt;path&gt;...

## DESCRIPTION

  Opens `<path>` in the GVim or Neovim instance identified by `<servername>`
  or `<socketname>` and positions the cursor at row `<line>` and column
  `<column>`.

## ENVIRONS

  You can use an environ instead to specify the `<servername>`
  or `<socketname>`

  - The server name is used for GVim, e.g., `gvim --servername <servername>`

  - The socket name is used for Neovim, e.g., `nvim --server /tmp/nvim.socket-<socketname>`

  The `servername` or `socketname` should be a simple alpha-numeric-emoji
  string (i.e., avoid using spaces and path separators).

  You can use different server and socket names to open files
  in different editor instances.

  - On GVim, you'll also see the ``--servername`` in the
    GVim titlebar, so you might enjoy customizing it.

  You can also define environs to use as defaults if the server or
  socket name is not specified as a command argument:

    export GVIM_OPEN_SERVERNAME="GVIM"

    export NVIM_OPEN_SOCKETNAME="NVIM"

## NEOVIM CHOOSER

  Call `nvim-open-kindess` to open files in Neovim.

  If the specified Neovim server is not running, the script starts
  a new editor process.

  The editor it starts can be customized using an environ variable,
  and defaults to running `nvim` in the console:

    export NVIM_OPEN_APPNAME="nvim"

  You might also prefer to run a GUI app, such as
  [Neovide](https://github.com/neovide/neovide):

    export NVIM_OPEN_APPNAME="neovide"

## EXAMPLES

  Open this README and position the cursor on line 31, column 39,
  using the default `--servername` specified by `GVIM_OPEN_SERVERNAME`:

    $ cd path/to/gvim-open-kindness
    $ bin/gvim-open-kindness "" "31" "39" "README.md"

  Open the same, but send to the GVim named "my-other-gvim":

    $ bin/gvim-open-kindness "my-other-gvim" "31" "39" "README.md"

  Likewise, but specifying the server name with an environ:

    $ GVIM_OPEN_SERVERNAME="my-other-gvim" bin/gvim-open-kindness "" "31" "39" "README.md"

## INSTALL

  Many users will be able to symlink `gvim-open-kindness` from
  user-local-bin to call it without using its full path, e.g.,:

    ln -sfn \
      "/full/path/to/gvim-open-kindness/bin/gvim-open-kindness" \
      "${HOME}/.local/bin/gvim-open-kindness"

  If you want to open files in Neovim instead of GVim, call
  the script using its pseudonym, `nvim-open-kindness`:

    ln -sfn \
      "/full/path/to/gvim-open-kindness/bin/gvim-open-kindness" \
      "${HOME}/.local/bin/nvim-open-kindness"

## OPTIONAL NOTIFICATION

  If you'd like a popup notification if there's an error:

  - On macOS, ensure `terminal-notifier` is available:

      `brew install terminal-notifier`

  - On Linux, ensure `notify-send` is available:

      `sudo apt install libnotify-bin`

  Otherwise errors are sent to a temp file.

  - This is so you can wire `gvim-open-kindness` from an OS-level
    keybinding (e.g., using Hammerspoon, or Karabiner-Elements)
    and still be able to diagnose errors.

## OPTIONAL DEPENDENCIES

### macOS window fronter — *Hammyspoony*

When you send a file to Vim or Neovim to open, the Vim
server app might not front itself on your desktop.

Some apps will, e.g., MacVim, but other apps won't,
e.g., Neovide, or running Neovim in the terminal.

If you'd like to find and front the Vim app when you
send it a file to open, install the `URISetFrontmost`
Hammerspoon Spoon:

https://github.com/DepoXy/macOS-Hammyspoony/blob/release/Source/URISetFrontmost.spoon/init.lua

found in this script's author's *HammySpoony* project:

https://github.com/DepoXy/macOS-Hammyspoony 🥄

You'll also need to print the `v:servername` value in the
titlebar, using `set title titlestring=...`, which you'll
find in this Vim plugin that also adds the T.O.D. to the
window title:

https://github.com/landonb/vim-title-bar-time-of-day 🕰️

The Hammerspoon mechanism finds and fronts any window
with the given server name, so ensure that
`GVIM_OPEN_SERVERNAME` and/or `NVIM_OPEN_SOCKETNAME`
are unique (and don't, e.g., conflict with any browser
window titles).

### Vim nice open plugin — `vim-buffer-delights`

When you send a file to Vim to open, it'll open in whatever
window is active.

If you'd like to avoid opening the file in a special buffer
window, e.g., the quickfix window, a help window, a `:netrw`
window, etc., install the `embrace-vim/vim-buffer-delights`
Vim plugin:

https://github.com/embrace-vim/vim-buffer-delights 🍧

If that plugin is not installed, `gvim-open-kindness` will still
work, but the file will be opened in whatever window has focus,
which might contain a special buffer. Such windows might have
peculiar dimensions or otherwise not be desirable to use for
editing.

The `vim-buffer-delights` plugin will wire a number of window and
buffer command maps, which you can disable with a global variable,
because this script calls an `autoload#` function:

    let g:vim_buffer_delights_disable = 1

## USE CASES

  This script pairs well with `rg` and `tag`.

## RELATED PROJECTS

- *Open a local file from a URL at a line number in an editor/IDE*

  (From the author of [`git-delta`](https://github.com/dandavison/delta).)

  https://github.com/dandavison/open-in-editor

## AUTHOR

**gvim-open-kindness** is Copyright (c) 2021-2025 Landon Bouma &lt;depoxy@tallybark.com&gt;

This software is released under the MIT license (see `LICENSE` file for more)

## REPORTING BUGS

&lt;https://github.com/DepoXy/gvim-open-kindness/issues&gt;

