# Alex's dotfiles

This repo was forked from Matt Mollison's [dotfiles](https://github.com/warmlogic/dotfiles), which borrows heavily from Mathias Bynens's [dotfiles](https://github.com/mathiasbynens/dotfiles/) and Dries Vints's [dotfiles](https://github.com/driesvints/dotfiles).

This also includes `tmux` files from [this repo](https://github.com/gpakosz/.tmux).

## Installation

**Warning:** If you want to give these dotfiles a try, you should first fork this repository, review the code, and remove things you don't want or need. Don't blindly use my settings unless you know what that entails. Use at your own risk!

Some of the functionality of these dotfiles depends on formulae installed by `02-brew.sh`. If you don't plan to run `02-brew.sh`, you should look carefully through the script and manually install any particularly important ones. A good example is Bash/Git completion: the dotfiles use a special version from Homebrew.

### Quick instructions overview

1. Update macOS to the latest version
1. Install the Xcode command line developer tools (required for `git`): `xcode-select --install`
1. While you're waiting, create credentials for this computer and add to GitHub.
    1. [Generate a new ssh key](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/): `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`
    1. [Log in to GitHub](https://github.com/login)
    1. [Add your new public key to your GitHub account settings](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) [here](https://github.com/settings/keys): `pbcopy < ~/.ssh/id_rsa.pub`
1. Clone this repo
    1. `mkdir -p ~/code/github/`
    1. `cd ~/code/github/`
    1. `git clone git@github.com:AlexGroves/dotfiles.git`
    1. `cd ~/github/dotfiles/`
1. Run `01-bootstrap.sh` to copy necessary files (hidden and otherwise)
1. `cp .extra ~/.extra` and edit, if desired (explained below)
1. If installing Mac App Store apps with Brew, sign in to the Mac App Store
1. Ensure `Brewfile` includes only the programs you want to install
    1. Run `02-brew.sh` to install apps (this script ensures the Xcode command line tools are installed before installing brew)
1. Run `03-macos.sh` to set up macOS preferences
1. Restart your computer
1. Run `04-python.sh` to set up a Python 3 conda environment named `py3`
1. Set up installed applications (look at `Brewfile` as a reminder of what was installed)
1. If needed, copy public and private ssh keys from previous computer to `~/.ssh/` and `chmod` to `600`
   - Set up `~/.ssh/config` to add ssh keys to Keychain ([instructions](https://github.com/jirsbek/SSH-keys-in-macOS-Sierra-keychain))
1. [Set up "Open in Safari or Chrome URL in Other Browser AppleScript + Automator Workflow](https://gist.github.com/warmlogic/e6b2f30640b4c5de2077373fb53f6df3)

More details below.

### Using Git and the bootstrap script

Clone the repository wherever you want (I keep it in `~/code/github/dotfiles`). The bootstrapper script (`01-bootstrap.sh`) will pull in the latest version and copy the files to your home folder. **You probably don't want to run the boostrap script the first time, since you'll want to update the settings for your environment**.

`cd` into your local `dotfiles` repository, and start the installation:

```bash
source 01-bootstrap.sh
```

### Specify the `$PATH`

If `~/.path` exists, it will be sourced along with the other files before any feature testing (such as [detecting which version of `ls` is being used](https://github.com/mathiasbynens/dotfiles/blob/aff769fd75225d8f2e481185a71d5e05b76002dc/.aliases#L21-26)) takes place.

Here's an example `~/.path` file that adds `/usr/local/bin` to the `$PATH`:

```bash
export PATH="/usr/local/bin:$PATH"
```

### Add custom commands without creating a new fork

If `~/.extra` exists, it will be sourced along with the other files. You can use this to add a few custom commands without the need to fork this entire repository, or to add commands you don't want to commit to a public repository.

NB: `~/.extra` is included in the repo, but it is not automatically copied over by `01-bootstrap.sh`. Therefore, you'll want to run the following command and edit the new file's contents:

```bash
cp .extra ~/.extra
```

You can also use `~/.extra` to override settings, functions, and aliases. It's probably better to [fork this repository](https://github.com/AlexGroves/dotfiles/fork) instead, though.

### Install Homebrew formulae

When setting up a new Mac, you may want to install some common [Homebrew](http://brew.sh/) formulae. This installs the Xcode command line developer tools, Homebrew, and everything listed in `Brewfile`.

```bash
./02-brew.sh
```

### Set macOS Preferences

When setting up a new Mac, you may want to set some sensible macOS defaults:

```bash
./03-macos.sh
```

### Python/Anaconda setup

You may also want Python 3 and a number of useful packages related to data analysis (via [miniconda](https://conda.io/miniconda.html)). This installs everything listed in `init/environment-py3.yml`.

```bash
./04-python.sh
```

### Additional setup

#### Calendar

- Add accounts with your calendars to Internet Accounts (System Preferences)
- Itsycal format: `h:mm a`, show day
- Turn off system clock

#### Safari Extensions

- [Wipr](https://apps.apple.com/us/app/wipr/id1320666476) (installed via `Brewfile`)
- [Clean Links for Google](https://apps.apple.com/us/app/clean-links-for-google/id1467225874) (installed via `Brewfile`)
- [Polyglot](https://apps.apple.com/us/app/polyglot/id1471801525) (installed via `Brewfile`)
  - Turn off Instant Translation

#### Visual Studio Code Extensions

- autoDocstring
- Beautify
- Brewfile
- Docker
- Dracula Official
- Excel Viewer
- GitLens
- LaTeX Workshop
- macros (for keybindings)
- Markdown All in One
- markdownlint
- parquet-viewer
- PostgreSQL
- Python
- python-string-sql
- Rainbow CSV
- Remote VSCode
- Spell Right
- SQLTools
- Terraform
- Todo Tree
- Visual Studio IntelliCode
- VS Code Jupyter Notebook Previewer

#### SublimeText Packages

- [Package Control](https://packagecontrol.io/installation)
- [Anaconda](http://damnwidget.github.io/anaconda/)
- [WordCount](https://github.com/titoBouzout/WordCount)
- [Pretty JSON](https://github.com/dzhibas/SublimePrettyJson)
- [MarkdownEditing](https://github.com/SublimeText-Markdown/MarkdownEditing)
  - Change color scheme to ArcDark
- [INI](https://github.com/clintberry/sublime-text-2-ini)
- [rsub](https://github.com/henrikpersson/rsub) ([see instructions](http://caitriggs.com/blog/using-sublime-text-editor-ec2-instance/))

Could use these for additional Python linting setup:

- [SublimeLinter](https://github.com/SublimeLinter/SublimeLinter)
- [SublimeLinter-contrib-mypy](https://github.com/fredcallaway/SublimeLinter-contrib-mypy)

#### Jupyter Notebook Extensions

(Note: Not updated for Jupyter Lab)

These should be automatically turned on, via `.jupyter/nbconfig/notebook.js`

- ExecuteTime
- spellchecker
- Table of Contents (2)
- Collapsible headings
- Highlight selected word
- Scroll down

## TODO

- Consider including an [IPython startup script](http://ipython.readthedocs.io/en/stable/interactive/tutorial.html?highlight=startup#startup-files).

## Feedback

Suggestions/improvements [welcome](https://github.com/AlexGroves/dotfiles/issues)!
