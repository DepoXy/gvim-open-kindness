gvim-open-kindness — Kindly file opener that positions your cursor 🐬
=====================================================================

## SYNOPSIS

`gvim-open-kindness` &lt;servername&gt; &lt;line&gt; &lt;column&gt; &lt;path&gt;...

## DESCRIPTION

  Opens `<path>` in the GVim identified by `<servername>`
  and positions the cursor at row `<line>` and column `<column>`

## ENVIRONS

  You can use an environ instead to specify the GVim `--servername`
  option, which identifies which GVim instance to open (see `man gvim`
  if you need more help).

  - The default `--servername` is "SAMPI" (for no particular reason).

  E.g., you might want to add this to your Bash or shell startup script:

    export GVIM_OPEN_SERVERNAME="my-gvim-server"

## EXAMPLES

  Open this README and position the cursor on the '4' in '49,
  using the default `--servername` specified by `GVIM_OPEN_SERVERNAME`:

    $ cd path/to/gvim-open-kindness
    $ bin/gvim-open-kindness "" "31" "39" "README.md"

  Open the same, but send to the GVim named "my-other-gvim":

    $ bin/gvim-open-kindness "my-other-gvim" "35" "52" "README.md"

  Likewise, but using the environ:

    $ GVIM_OPEN_SERVERNAME="my-other-gvim" bin/gvim-open-kindness "" "39" "76" "README.md"

## INSTALL

  Many users will be able to symlink `gvim-open-kindness` from
  user-local-bin to call it without using its full path, e.g.,:

    /bin/ln -sfn \
      "/full/path/to/gvim-open-kindness/bin/gvim-open-kindness" \
      "${HOME}/.local/bin/gvim-open-kindness"

## OPTIONAL

  If you'd like a popup notification if there's an error:

  - On macOS, ensure `terminal-notifier` is available:

      `brew install terminal-notifier`

  - On Linux, ensure `notify-send` is available:

      `sudo apt install libnotify-bin`

  Otherwise errors are sent to a temp file.

  - This is so you can wire `gvim-open-kindness` from an OS-level
    keybinding (e.g., using Karabiner-Elements) and still be able
    to diagnose errors.

## USE CASES

  This script pairs well with `rg` and `tag`.

## AUTHOR

**gvim-open-kindness** is Copyright (c) 2021-2023 Landon Bouma &lt;depoxy@tallybark.com&gt;

This software is released under the MIT license (see `LICENSE` file for more)

## REPORTING BUGS

&lt;https://github.com/DepoXy/gvim-open-kindness/issues&gt;

