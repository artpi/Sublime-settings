# BASH Command line

* `ln -s KATALOG_DOCELOWY ./NAZWA_LINKA`
* `find . -iname '*something*'` - szukaj pliku
* `locate something` - szukaj pliku gdziekolwiek



# Komendy
* awk '{ x += $3 } END { print x }' myfile - Summing all numbers in the third column of a text file
- `lynx -dump -stdin` - HTML to text
- `nl`: add line numbers
- `bc`: calculator
- `stat`: file info
- `screen`: powerful terminal multiplexing and session persistence
- `look`: find English words (or lines in a file) beginning with a string
- `cut `and paste and join: data manipulation
- `fmt`: format text paragraphs
- `pr`: format text into pages/columns
- `fold`: wrap lines of text
- `column`: format text into columns or tables
- `expand `and unexpand: convert between tabs and spaces
- `cal`: nice calendar
- `iconv `or uconv: conversion for text encodings
- `strings`: extract text from binary files


## Development
* [ag](https://github.com/ggreer/the_silver_searcher) - Super fast string search through a directory hierarchy
* [jq](https://github.com/stedolan/jq) - Sed for json data. You can use it to slice and filter and map and transform structured data
* [httpie](https://github.com/jakubroztocil/httpie) - HTTPie is a command line HTTP client, a user-friendly cURL replacement
* [resty](https://github.com/micha/resty) - Little command line REST client that you can use in pipelines


## Multimedia

* [image-scraper](https://github.com/sananth12/ImageScraper) - A cool command line image scraper with a lot of features.
* [sejda](https://github.com/torakiki/sejda/) - Command line manipulation of PDF documents (split, merge, rotate, convert to jpg, extract text, etc)




## Narzędzia
* [Dropbox-Uploader](https://github.com/andreafabrizi/Dropbox-Uploader) - Dropbox Uploader is a Bash script which can be used to upload, download, list or delete files from Dropbox
* [youtube-dl](https://github.com/rg3/youtube-dl) - Small command-line program to download videos from YouTube.com and other video sites
* [cv](https://github.com/Xfennec/cv) - Linux tool to show progress for cp, rm, dd, ...
* [lsp](https://github.com/dborzov/lsp) - An improved `ls`, with file descriptions in plain language and intelligent file grouping
* [tmux](http://tmux.sourceforge.net/) - Amazing terminal multiplexer


## Customization

*Custom prompts, color themes, etc.*

* [base16-shell](https://github.com/chriskempson/base16-shell) - Base16 for Shells
* [bash-git-prompt](https://github.com/magicmonty/bash-git-prompt) - An informative and fancy Bash prompt for Git users
* [bash-powerline](https://github.com/riobard/bash-powerline) - Powerline-style Bash prompt in pure Bash script
* [bashstrap](https://github.com/barryclark/bashstrap) - A quick way to spruce up OSX terminal
* [flatui-terminal-theme](https://dribbble.com/shots/1021755-Flat-UI-Terminal-Theme) - Nicer colors for terminal
* [git-prompt](https://github.com/lvv/git-prompt) - Bash prompt with Git, SVN and HG modules
* [gittify](https://github.com/momeni/gittify) - A colorful Bash prompt + customized Git aliases
* [Gogh - Color Scheme](https://github.com/Mayccoll/Elementary-OS-Terminal-Colors) - Color Scheme for Gnome Terminal
* [liquidprompt](https://github.com/nojhan/liquidprompt) - A full-featured & carefully designed adaptive prompt for Bash & Zsh
* [mysql-colorize](https://github.com/horosgrisa/mysql-colorize.bash) -  Colorization for mysql comand-line client
* [sexy-bash-prompt](https://github.com/twolfson/sexy-bash-prompt) - Bash prompt with colors, Git statuses, and Git branches


# To learn

- xargs

- Know basic `awk` and `sed` for simple data munging. For example, summing all numbers in the third column of a text file: `awk '{ x += $3 } END { print x }'`. This is probably 3X faster and 3X shorter than equivalent Python.


- Be familiar with bash job management: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- In bash, use **ctrl-r** to search through command history.

- In bash, use **ctrl-w** to delete the last word, and **ctrl-u** to delete the whole line. Use **alt-Left** and **alt-Right** to move by word, and **ctrl-k** to kill to the end of the line. See `man readline` for all the default keybindings in bash. There are a lot. For example **alt-.** cycles through previous arguments, and **alt-*** expands a glob.

- To go back to the previous working directory: `cd -`

- If you are halfway through typing a command but change your mind, hit **alt-#** to add a `#` at the beginning and enter it as a comment (or use **ctrl-a**, **#**, **enter**). You can then return to it later via command history.

- Use `xargs` (or `parallel`). It's very powerful. Note you can control how many items execute per line (`-L`) as well as parallelism (`-P`). If you're not sure if it'll do the right thing, use `xargs echo` first. Also, `-I{}` is handy. Examples:
```
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` is a helpful display of the process tree.

- Use `pgrep` and `pkill` to find or signal processes by name (`-f` is helpful).

- Know the various signals you can send processes. For example, to suspend a process, use `kill -STOP [pid]`. For the full list, see `man 7 signal`

- Use `nohup` or `disown` if you want a background process to keep running forever.

- Check what processes are listening via `netstat -lntp`.

- See also `lsof` for open sockets and files.

- In bash scripts, use `set -x` for debugging output. Use strict modes whenever possible. Use `set -e` to abort on errors. Use `set -o pipefail` as well, to be strict about errors (though this topic is a bit subtle). For more involved scripts, also use `trap`.

- In bash scripts, subshells (written with parentheses) are convenient ways to group commands. A common example is to temporarily move to a different working directory, e.g.
```
      # do something in current dir
      (cd /some/other/dir; other-command)
      # continue in original dir
```

- In bash, note there are lots of kinds of variable expansion. Checking a variable exists: `${name:?error message}`. For example, if a bash script requires a single argument, just write `input_file=${1:?usage: $0 input_file}`. Arithmetic expansion: `i=$(( (i + 1) % 5 ))`. Sequences: `{1..10}`. Trimming of strings: `${var%suffix}` and `${var#prefix}`. For example if `var=foo.pdf`, then `echo ${var%.pdf}.txt` prints `foo.txt`.

- The output of a command can be treated like a file via `<(some command)`. For example, compare local `/etc/hosts` with a remote one:
```
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Know about "here documents" in bash, as in `cat <<EOF ...`.

- In Bash, redirect both standard output and standard error via: `some-command >logfile 2>&1`. Often, to ensure a command does not leave an open file handle to standard input, tying it to the terminal you are in, it is also good practice to add `</dev/null`.

- Use `man ascii` for a good ASCII table, with hex and decimal values.

- Use `screen` or `tmux` to multiplex the screen, especially useful on remote ssh sessions and to detach and re-attach to a session. A more minimal alternative for session persistence only is `dtach`.

- In ssh, knowing how to port tunnel with `-L` or `-D` (and occasionally `-R`) is useful, e.g. to access web sites from a remote server.

- It can be useful to make a few optimizations to your ssh configuration; for example, this `~/.ssh/config` contains settings to avoid dropped connections in certain network environments, and use compression (which is helpful with scp over low-bandwidth connections):
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
```

- A few other options relevant to ssh are security sensitive and should be enabled with care, e.g. per subnet or host or in trusted networks: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- To get the permissions on a file in octal form, which is useful for system configuration but not available in `ls` and easy to bungle, use something like
```
      stat -c '%A %a %n' /etc/timezone
```

- For interactive selection of values from the output of another command, use [`percol`](https://github.com/mooz/percol).

- For interaction with files based on the output of another command (like `git`), use `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).




# Guides

* [Bash Hackers Wiki](http://wiki.bash-hackers.org/)
* [Greg Wooledge's (aka "greycat") wiki](http://mywiki.wooledge.org).
  Specifically [Bash Guide](http://mywiki.wooledge.org/BashGuide), [Bash FAQ](http://mywiki.wooledge.org/BashFAQ) and [Bash Pitfalls](http://mywiki.wooledge.org/BashPitfalls)
* [Google's Shell Style Guide](https://google-styleguide.googlecode.com/svn/trunk/shell.xml)
* [The Linux Documentation Project: Bash Programming - Intro/How-to](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html#toc)
* [The Linux Documentation Project: Advanced Bash Scripting Guide](http://www.tldp.org/LDP/abs/html/)
* [WikiBooks: Bash Shell Scripting](http://en.wikibooks.org/wiki/Bash_Shell_Scripting)
* [Use the Unofficial Bash Strict Mode (Unless You Looove Debugging)](http://redsymbol.net/articles/unofficial-bash-strict-mode/)
* [The Art of Command Line](https://github.com/jlevy/the-art-of-command-line)
* [awesome-shell](https://github.com/alebcay/awesome-shell): A curated list of shell tools and resources.



