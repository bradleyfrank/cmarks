# cmarks

`cmarks` is *command line bookmarks*. Use this Zsh script to quickly save useful or important commands to a centralized location.

## Installation

Requirements:

* [`zsh`](https://www.zsh.org/)
* [`fzf`](https://github.com/junegunn/fzf)
* [`gh`](https://github.com/cli/cli) (to use the built-in Gist sync)

To get started:

1. Save the `cmarks` file locally
2. Add `source path/to/cmarks` to your `.zshrc`

To use sync:

* Through GitHub.com:
   1. Create a GitHub Gist (private or public)
   2. Note the hash ID (in the url)
   3. Add the Gist hash ID to the config file
* With `cmarks`:
  1. Run `cmarks -z [private|public]` (this will automatically update the config)

## Configuration

To override the default config location (`~/.config/cmarks.cfg`), add `export CMARKS_CONFIG=/my/cmarks/config` before sourcing.

Options for the config file are as follows:

```text
cmarks_file=
github_gist_id=
```

## Usage

```text
Usage: cmarks [OPTION]
-a <num1>[,<num2>]    Add command(s) from history to bookmarks
-d <num1>[,<num2>]    Delete bookmarked command(s)
-f                    Find bookmarked command(s) and append to history
-g <num1>[,<num2>]    Get bookmarked command(s) and append to history
-h                    Show help and usage
-l                    List all bookmarked commands
-p <num1>[,<num2>]    Print bookmarked command(s) to stdout
-s push|pull          Sync bookmarks with GitHub Gist
-z public|private     Create new GitHub Gist for syncing (default: private)
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
