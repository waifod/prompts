# Tools

Preferred CLI tools by platform. Use the best available tool for the environment; fall back when something is not installed.

Dotfiles (personal machines only): [github.com/waifod/dotfiles](https://github.com/waifod/dotfiles)

The Cloud Desktop is a vanilla Amazon configuration. No custom tooling, no dotfiles. Standard coreutils, standard shell, standard everything. The personal machines are the customized ones.

## Common Rules

- Use non-interactive flags. Never leave a command waiting for input.
- Use timeouts: `timeout <seconds> <command>` (on macOS, requires `coreutils` via Homebrew).

## Platform Matrix

| Task | Arch / Fedora | macOS | Cloud Desktop |
|---|---|---|---|
| Search file contents | `rg` (ripgrep) | `rg` (ripgrep) | `grep` (`rg` available) |
| Find files | `fd` | `fd` | `find` |
| View files | `bat` | `bat` | `cat` |
| List files | `eza` | `eza` | `ls` |
| Disk usage | `dust` | `dust` | `du` |
| Directory navigation | `zoxide` (`cd` is aliased) | `cd` | `cd` |
| System monitor | `btm` (bottom) | `btm` (bottom) | `top` |
| Git pager/diff | `delta` (side-by-side) | `delta` (side-by-side) | standard git pager |
| Man pages | `batman` (bat-extras) | `batman` (bat-extras) | `man` |

## Shell Aliases

These are active on Arch, Fedora, and macOS (defined in `.zsh_aliases`). On Cloud Desktop, the standard commands apply.

```
cat   -> bat --paging=never
less  -> bat
du    -> dust
find  -> fd
grep  -> rg
ls    -> eza
```

The `man` function (`.zsh_functions`) resolves aliases before looking up manpages via `batman`, so `man cat` shows the `bat` manpage.

## Runtime and Package Management

| Tool | Purpose | Platforms |
|---|---|---|
| `mise` | Runtime version manager (Node LTS via config) | All personal |
| `uv` | Python package manager; `python` and `pip` are aliased to `uv run python` and `uv pip` | All personal |
| `sheldon` | Zsh plugin manager (loads `fzf-tab`) | All personal |
| Homebrew | macOS system packages | macOS only |

## Git Configuration

Global git config uses:
- `delta` as core pager (side-by-side, line numbers, gruvbox-dark theme)
- `histogram` diff algorithm, `zdiff3` merge conflict style
- SSH signing (ed25519), commit and tag signing enabled
- `fsmonitor` and `untrackedCache` for performance
- Auto-stash on rebase, auto-squash, prune on fetch

## Remote Build and Sync

The Cloud Desktop has more CPU and memory than the laptop. Prefer building there, especially for large packages. Use `remote-build` from macOS to run builds on the Cloud Desktop without switching context.

Custom scripts in `~/.local/bin/` (personal machines only):

- `remote-build <amazon|hetzner> [command]`: SSH into a remote machine and run a build command in the corresponding directory. Defaults to `brazil-build release` for Amazon, `make` for Hetzner. Only Amazon remote is available from macOS.
- `remote-sync <amazon|hetzner> [options]`: Unison-based file sync with remote machines. Supports continuous sync, one-shot (`-o`), interactive (`-i`), and force direction (`-f remote` or `-f local`).

macOS aliases:
```
rbb   -> remote-build amazon                     # brazil-build release on cloud desktop
rbbt  -> remote-build amazon brazil-build test    # brazil-build test on cloud desktop
rhb   -> remote-build hetzner                     # make on Hetzner
```

## Editor

`nvim` is the default editor (`$EDITOR` and `$VISUAL`) on personal machines (Arch, Fedora, macOS). Cloud Desktop uses the Amazon default.
