# Productivity

A set of tools and script for a powerful bash experience in production

## General features

Productivity (alias prdvty), is a library for bash 4.2+, aimed at improving your Linux shell experience.
It provides and configure some tools, and can be extended by your own script placed 

## Features

Most visible features are:
- Dynamic and meaningful prompt (powerline)
- Enhanced search engine, used for history search (fzf)
- Quick folder change, based on last-recently or mostly visited folder (z)
- bash environment improvements: history, completion

The 3rd party scripts are not modified, so we can update them easily.
Instead, we leverage their environment variables before & after their loading

### powerline: Colorful prompt

An implementation of [b-ryan/powerline-shell](https://github.com/b-ryan/powerline-shell) in pure bash.
No need for python, daemon or any other dependency.

### fzf: Fuzzy Completion

An improved fuzzy search tool: you don't need to know the exact part, just pieces of it are enough to find and select it.
Binds as the history (Ctrl+R) when loaded.

### z: Jump around the previous folders

A shortcut to jump among your last or most often visited folder.


## Customization & Inner Workings

When you load the main `productivity` script, it will load files matchingfollowing glob patterns:
  1. `lib/local/lib.pre/*.lib`
  2. `lib/prdvty/*.lib`
  3. `lib/local/lib.post/*.lib`
  4. `modules/*/lib/*`

The `lib/local` folder is left empty so you can place your own files.



## Credits

prdvty:
- Adrien Mahieux / Prod365

Third Party:
- **fzf**:  Junegunn Choi - https://github.com/junegunn/fzf - [MIT](https://github.com/junegunn/fzf/blob/master/LICENSE)
- **powerline.bash**: Etienne BERSAC - https://gitlab.com/bersace/powerline.bash - [The Unlicense](https://unlicense.org)
- **z**: Rupa. https://github.com/rupa/z - [WTFPL](https://github.com/rupa/z/blob/master/LICENSE)
