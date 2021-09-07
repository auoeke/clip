clip is a simple clipboard manager that does not depend on a window system like X. I made it for my headless server.

The path of the clipboard file is [`${TMPDIR:-/tmp}/clipboard`](https://www.gnu.org/software/bash/manual/html_node/Shell-Parameter-Expansion.html).

`clip` and `setclip` should be executable and in a directory in `$PATH`.

`clip` is the primary user interface to the clipboard. When run without arguments, it outputs the contents of the clipboard; when run with arguments, it sets the clipboard to them.

`setclip` reads stdin and sets the clipboard to its contents.

```sh
$ clip test0
$ clip
test0
```
```sh
$ setclip <<< "test1"
$ clip
test1
```

### Neovim
Neovim can be configured to use `clip` and `setclip` by setting `g:clipboard` in `${XDG_CONFIG_DIR:-$HOME/.config}/nvim/init.vim`:
```vim
let g:clipboard = {
            \     'name': 'clip',
            \     'copy': {
            \         '+': ['setclip'],
            \         '*': ['setclip'],
            \     },
            \     'paste': {
            \         '+': ['clip'],
            \         '*': ['clip'],
            \     },
            \ }
```
