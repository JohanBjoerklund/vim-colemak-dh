vim-colemak-dh
===========

Colemak-dh key mappings for Vim. Trimmed and modified version of [Shai Coleman's configuration](http://colemak.com/pub/vim/colemak.vim).

Install
-------

1. Use [vim-plug](https://github.com/junegunn/vim-plug).
2. Add to `.vimrc`: `Plug 'jooize/vim-colemak'`
3. Run `vim +PlugInstall`
4. You probably want to load vim-colemak-dh last. Reload the plugin at the bottom of your Vim configuration.

    ```
    " Reload vim-colemak to remap any overridden keys
    silent! source "$HOME/.vim/bundle/vim-colemak-dh/plugin/colemak-dh.vim"
    ```

    *Note: You might be using `~/.vim/plugged`.*

5. See [issues](#issues) for conflicts with other plugins.

Key mappings
------------

```
Colemak layout:                  |                 QWERTY layout:
`12345 67890-=     Move around:  |  (instead of)   `12345 67890-=
 qwfpb jluy;[]\         e        |       k          qwert yuiop[]\
 arstg MNEIo'         m   i      |     h   l        asdfg HJKL;'
 zxcdv kh,./            n        |       j          zxcvb nm,./

(  novx)  m = h (Left)     i = l (Right)     e = k (Up)     n = j (Down)

(  novx)  l = b (Back word)            L = B (Back WORD)
(  novx)  y = w (Forward word)         Y = W (Forward WORD)
(  novx)  u = e (Forward end of word)  U = E (Forward end of WORD)

(c     )  <C-L> = <C-Left> (Back WORD)
(c     )  <C-Y> = <C-Right> (Seems to equal forward WORD minus 1 character)

(  n  x)  a = v (Visual)   A = V (Visual line)
(  n   )  r = r (Replace)  R = R (Replace)
(  n   )  s = i (Insert)   S = I (Insert before first non-blank of line)
(  n   )  t = a (Append)   T = A (Append at end of line)
(  n   )  w = c (Change)   W = C (Change to end of line)  ww = cc (Change line)

(  n  x)  z = u (Undo)    Z = <C-R> (Redo)  gz = U (Undo all latest changes on line)
(  n  x)  x = x (Cut)     X = dd (Cut line)
(  n  x)  c = y (Copy)    C = yy (Copy line)
(  n  x)  v = p (Paste)   V = P (Paste)
(  n  x)  gv = gp (Paste) gV = gP (Paste)

(   o  )  r = i (Example: dip -> drp (Delete inner paragraph))

(  no x)  p = t{char} (Before next {char})  P = T{char} (After previous {char})
(  no x)  b = ; (Repeat latest f or t)  B = , (Repeat latest f or t reversed)
(  no x)  k = n (Repeat latest / or ?)  K = N (Repeat latest / or ? reversed)

(  n  x)  j = z
(  n  x)  jn = zj (Next fold) [Also jj = zj]
(  n  x)  je = zk (Previous fold) [Also jk = zk]

(  n   )  ga = gv (Reselect last visual selection)
(  n  x)  gK = K (Lookup)
(  n  x)  gL = L (To line [count] from bottom of window)

(  n  x)  <C-W>m = <C-W>h (Window left)
(  n  x)  <C-W>n = <C-W>j (Window down)
(  n  x)  <C-W>e = <C-W>k (Window up)
(  n  x)  <C-W>i = <C-W>l (Window right)

Lost:
(  n  x)  s (Substitute [count] characters) [Use wi = cl]
(  n  x)  S (Substitute [count] lines) [Use ww = cc]
(  n  x)  X (Cut [count] characters backwards) [Use dh = dh]
(  n   )  Z (Quit)
(  n  x)  <C-W>n (Window down) [Use <C-W><C-N> = <C-W><C-N>]
(  n  x)  <C-W>i (Window down) [Use <C-W><C-I> = <C-W><C-I>]

Legend:
<C-X>     Ctrl-X
(c     )  Command-line mode
( i    )  Insert mode
(  n   )  Normal mode
(   o  )  Operator pending
(    v )  Visual+Select mode
(     x)  Visual mode
```

Issues
------

### [tpope/vim-fugitive](https://github.com/tpope/vim-fugitive) keymap collision

    " Fix for colemak.vim keymap collision. tpope/vim-fugitive's maps y<C-G>
    " and colemak.vim maps 'y' to 'w' (word). In combination this stalls 'y'
    " because Vim must wait to see if the user wants to press <C-G> as well.
    augroup RemoveFugitiveMappingForColemak
        autocmd!
        autocmd BufEnter * silent! execute "nunmap <buffer> <silent> y<C-G>"
    augroup END

Changes
-------

### 2016–03–06

- [Restore wrapped line behavior to Vim default (e.g. n = gj is now n = j)](https://github.com/jooize/vim-colemak/commit/6882195551f1025e72f352811ea7b331bc73b32e)
- [Remove turbo navigation (HNEI are now unmapped)](https://github.com/jooize/vim-colemak/commit/c057ed04075cab3f0a67c0fdc30c9d2f35621eff)
- [Add missing mapping for reselecting last visual selection (ga = gv)](https://github.com/jooize/vim-colemak/commit/5167bbf4c411fd765833c97bfc078bed53cc995e)

#### Restore turbo navigation

Add the following to your `.vimrc`:

```
" Turbo navigation (Colemak) {{{
    " Works with counts, see ":help complex-repeat"
    nnoremap <silent> H @='5h'<CR>|xnoremap <silent> H @='5h'<CR>|onoremap <silent> H @='5h'<CR>|
    nnoremap <silent> N @='5gj'<CR>|xnoremap <silent> N @='5gj'<CR>|onoremap <silent> N @='5gj'<CR>|
    nnoremap <silent> E @='5gk'<CR>|xnoremap <silent> E @='5gk'<CR>|onoremap <silent> E @='5gk'<CR>|
    nnoremap <silent> I @='5l'<CR>|xnoremap <silent> I @='5l'<CR>|onoremap <silent> I @='5l'<CR>|
" }}}
```

I removed turbo navigation since I felt it doesn't suit as default Vim mappings, which also frees up the keys for custom uses. I'm considering making it an option. [Discuss!](https://github.com/jooize/vim-colemak/issues/4)
