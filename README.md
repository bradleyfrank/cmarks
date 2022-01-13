# cmarks

`cmarks` is *command line bookmarks*. Use this Zsh script to quickly save useful or important commands to a centralized location.

## Installation

Requirements:

* [`zsh`](https://www.zsh.org/)
* [`fzf`](https://github.com/junegunn/fzf)
* [`gh`](https://github.com/cli/cli) (to use the built-in Gist sync)

To get started:

1. Save the `cmarks` file locally
2. Add `source /path/to/cmarks` to your `.zshrc`

To use sync:

1. Create a GitHub Gist (private or public) and note the hash ID (in the url)
2. Add the Gist hash ID to the config file

## Configuration

To override the default config location (`~/.config/cmarks`), add `export CMARKS_CONFIG=/my/cmarks/config` before sourcing `cmarks`.

Options for the config file are as follows:

```text
CMARKS_FILE=
CMARKS_GIST=
```

## Usage

```text
Usage: cmarks [OPTION]
-a <num1>[,<num2>]    Add commands from history
-d <num1>[,<num2>]    Delete commands from bookmarks
-f                    Use fzf to find commands in bookmarks and append to history
-g <num1>[,<num2>]    Get commands from bookmarks and append to history
-l                    List all commands in bookmarks
-p <num1>[,<num2>]    Print commands to stdout from bookmarks
-s push|pull          Sync bookmarks with GitHub gist
```

### Examples

Find the history index number for a recent command:
`fc -l`

Add a single command to cmarks (also works for delete/get/print):
`cmarks -a <num>`

Add the previous command to cmarks:
`cmarks -a -1`

Add a range of commands to cmarks (also works for delete/get/print):
`cmarks -a <num1>,<num2>`

## Notes

* Bookmarked commands have separate index numbers than shell history
* Index numbers are re-assigned when bookmarks are removed
* Sync is rudimentary, use with caution
