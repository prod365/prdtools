
# Productivity

A set of tools and script for a powerful bash experience in production

## General features

Productivity (alias prdvty), is a library for bash 4.2+, aimed at improving your Linux shell experience.
It provides and configure some tools, and can be extended by your own script placed 


## Features

Most visible features are:
- Dynamic and meaningful prompt (powerline)
- Enhanced search engine, used for history search (fzf)
- Quick folder navigation, based on last-recently or mostly visited folder (z)
- bash environment improvements: history per host (eg for NFS homedir), better completion

The 3rd party scripts are not modified, so we can update them easily.
Instead, we leverage their environment variables before & after their loading.

Custom modules can be easily loaded on startup, or before/after every command.

### powerline: Colorful prompt

Pure bash implementation of [b-ryan/powerline-shell](https://github.com/b-ryan/powerline-shell).
No need for python, daemon or any other dependency.

Some helper functions are added:
  - `prdvty::powerlineSegmentAdd (newSegment) [addBefore]`: Add a segment, optionally before another one.
  - `prdvty::powerlineSegmentDel (delSegment) [...]`: Delete one or more provided segments.

### fzf: Fuzzy Completion

An improved fuzzy search tool: you don't need to know the exact part, just pieces of it are enough to find and select it.
Binds as the history (Ctrl+R) when loaded.

### z: Jump around the previous folders

A shortcut to jump among your most frequently or recently visited folder.



### bash upgrades

Readline updates: using `bind` command, we can change readline features without using a `.inputrc` file:
  - `set show-all-if-ambiguous on`: display multiple possibilities with tab (no need to "double" tab)
  - `set completion-ignore-case on`: ignore case when using tab for completion
  - `set colored-completion-prefix on`: display the matched part in color to identify easily the missing part

bash history:
  - Set history file as `~/.bash_history.d/$(uname -n)`
  - Increase history to 999999 elements
  - Save date-time of each command in history as `[ %F %T ]`
  - Ignore repeated commands, and commands starting with a space

bash debug:
  - Pre & Post exec hooks: you can analyze and stop commands being run in your shell. See `prdvty::shell*ExecRegister` below
  - `PS4`: Improves debug-ability of shell scripts showing file, line and function of each command being run.


## Customization & Inner Workings

When you load the main `productivity` script, it will load files matching glob patterns:
  1. `lib/local/lib.pre/*.lib`
  2. `lib/prdvty/*.lib`
  3. `lib/local/lib.post/*.lib`
  4. `modules/*/lib/*`

The `lib/local` folder is left empty so you can place your own files.

You can also call custom functions before & after every shell command using:
  - `prdvty::shellPreExecRegister`: Add a function to call before running command. A return code != 0 will stop the execution of the command entered by the shell user. Use `$BASH_COMMAND` to get the command being run.
  - `prdvty::shellPostExecRegister`: Add a function to call after running a command, like those usually set in `$PROMPT_COMMAND`

## Modules

Some modules are provided by default, and can serve as example to implement your own.


### Kubernetes

Activated when `kubectl` is available. Whenever a `kubeconfig` file is found in the hierarchy of your current working dir,
the `KUBECONFIG` variable will be set to this file (the closest from your cwd).

A few scripts are provided under `kube*` aliases.



## Credits

prdvty:
- Adrien Mahieux / Prod365

Third Party:
- **fzf**:  Junegunn Choi - https://github.com/junegunn/fzf - [MIT](https://github.com/junegunn/fzf/blob/master/LICENSE)
- **powerline.bash**: Etienne BERSAC - https://gitlab.com/bersace/powerline.bash - [The Unlicense](https://unlicense.org)
- **z**: Rupa. https://github.com/rupa/z - [WTFPL](https://github.com/rupa/z/blob/master/LICENSE)
