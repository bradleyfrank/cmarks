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
-B                    Add command(s) from history to bookmarks [uses fzf]
-b <num1>[-<num2>]    Add command(s) from history to bookmarks
-D                    Delete bookmarked command(s) [uses fzf]
-d <num1>[-<num2>]    Delete bookmarked command(s)
-h                    Show help and usage
-l                    List all bookmarked commands
-P                    Print bookmarked command(s) to stdout [uses fzf]
-p <num1>[-<num2>]    Print bookmarked command(s) to stdout
-R                    Get bookmarked command(s) and append to history [uses fzf]
-r <num1>[-<num2>]    Get bookmarked command(s) and append to history
-s push|pull          Sync bookmarks with GitHub Gist
-z public|private     Create new GitHub Gist for syncing (default: private)
```

### Examples

1. Find the history index number for a recent command:

   ```sh
   % fc -l
    2387  glow README.md
    2388  podman machine start
    2389  podman pull fedora
    2390  podman run -it fedora bash
    2391  podman machine stop
   ```

2. Add a command to cmarks:

   ```sh
   % cmarks -a 2388
   % cmarks -l
      1 2022-15-01 13:20  podman machine start
   ```

   You can also reference previous commands with negative numbers:

   ```sh
   % cmarks -a -1
   % cmarks -l
      1 2022-15-01 13:30  podman machine stop
   ```

   Or use a range to capture multiple commands:

   ```sh
   % cmarks -a 2388,2390
   % cmarks -l
      1 2022-15-01 13:20  podman machine start
      2 2022-15-01 13:25  podman pull fedora
      3 2022-15-01 13:30  podman run -it fedora bash
   ```

3. Print a bookmarked command:

   ```sh
   % cmarks -p 3
   podman run -it fedora bash
   ```

4. Get a bookmarked command and append to history:

   ```sh
   % fc -l
    2476  ansible-lint playbooks/site.yml
    2477  ansible-playbook playbooks/site.yml
   % cmarks -g 2
   ```

   Press `↑` to quickly access the command. You can also see the command in your history:

   ```sh
   % fc -l
    2476  ansible-lint playbooks/site.yml
    2477  ansible-playbook playbooks/site.yml
    2478  cmarks -g 2
    2479  podman pull fedora
   ```

5. Delete a bookmarked command:

   ```sh
   % cmarks -d 2
   % cmarks -l
      1 2022-15-01 13:20  podman machine start
      2 2022-15-01 13:30  podman run -it fedora bash
   ```

## Notes

* Bookmarked commands have separate index numbers than shell history
* Index numbers are re-assigned when bookmarks are removed
* Sync is rudimentary, use with caution
