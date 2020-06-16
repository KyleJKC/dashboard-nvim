<div align="center">
<img src="https://user-images.githubusercontent.com/41671631/84760810-26c02480-affb-11ea-903a-d8796189e58a.png">
</div>
<div align="center">
<img src="https://user-images.githubusercontent.com/41671631/84384273-4f71a400-ac20-11ea-8806-8052ed64f28b.png" width="704" height="507">
</div>

<p align="center">
  <b><a href="https://github.com/hardcoreplayers/dashboard-nvim/wiki">Demo Screenshots</a></b>
  |
  <b><a href="/doc/dashboard.txt">doc</a></b>
</p>

## Install

- vim-plug

  ```vim
  Plug 'hardcoreplayers/dashboard-nvim'
  ```

- dein

  ```vim
  call dein#add('hardcoreplayers/dashboard-nvim')
  ```

## Options

- Config your excute tool by `g:dashboard_default_executive`,This option mean what fuzzy
  search plugins that you used. [vim-clap](https://github.com/liuchengxu/vim-clap)
  and [fzf.vim](https://github.com/junegunn/fzf.vim)
  [leaderf](https://github.com/Yggdroot/LeaderF)

  ```viml
  let g:dashboard_default_executive ='clap' --default
  ```

- Dashboard wrap some `vim-clap` and `fzf.vim` commands with window config, And
  the dashboard commands execute tool depends on what plugin you used

  - DashboardFindFile same as
    - vim-clap: `Clap history Clap files ++finder=rg --ignore --hidden --files`
    - fzf.vim : `Files`
  - DashboardFindHistory same as
    - vim-clap: `Clap history`
    - fzf.vim : `History`
  - DashboardChangeColorscheme same as
    - vim-clap: `Clap colors`
    - fzf.vim : `Colors`
  - DashboardFindWord same as
    - vim-clap: `Clap grep2`
    - fzf.vim : `Rg`
  - DashboardJumpMark same as
    - vim-clap: `Clap marks`
    - fzf.vim : `Marks`

  If you already define the vim-clap and fzf commands, just set your keymaps
  into the `g:dashboard_custom_shortcut`.
  If you want use the Dashboard wrap commands. you can define the dashboard
  commands keymap then set it into `g:dashboard_custom_shutcut`

  ```viml
  eg : "SPC mean the leaderkey
      let g:dashboard_custom_shortcut={
        \ 'last_session'       : 'SPC s l',
        \ 'find_history'       : 'SPC f h',
        \ 'find_file'          : 'SPC f f',
        \ 'change_colorscheme' : 'SPC t c',
        \ 'find_word'          : 'SPC f a',
        \ 'book_marks'         : 'SPC f b',
        \ }
  ```

  - what does the shortcut do? just a tip like `whichkey`,on dashboard you just
    move the cursor and press `enter`

- `g:dashboard_custom_header` custom the dashboard header (same as startify)

- `g:dashboard_custom_footer` custom the dashboard footer (same as startify)

- Dashboard provide session support with `SessionLoad` and `SessionSave`
  commands you can define keymap like this .
  ```viml
  nmap <Leader>ss :<C-u>SessionSave<CR>
  nmap <Leader>sl :<C-u>SessionLoad<CR>
  ```
  set the `dashboard_session_directory` to change the session folder
  default is `~/.cache/vim/session`
- Highlight group
  ```VimL
  DashboardHeader
  DashboardCenter
  DashboardShortcut
  DashboardFooter
  ```
- Autocmd `Dashboard` `DashboardReady` same as vim-startify

- `g:dashboard_custom_section` custom section, it's very easy to custom. like
  example.

  ```viml
  let g:dashboard_custom_section={
    \ 'buffer_list': [' Recently lase session                 SPC b b'],
    \ }

  function! BUFFER_LIST()
    Clap buffers
  endfunction
  ```

## Minial vimrc

you can replace the vim-clap or fzf.vim commands by dashboard commands

- dashboard-nvim with vim-clap

  ```viml
  Plug 'hardcoreplayers/dashboard-nvim'
  Plug 'liuchengxu/vim-clap'

  let g:mapleader="\<Space>"
  nmap <Leader>ss :<C-u>SessionSave<CR>
  nmap <Leader>sl :<C-u>SessionLoad<CR>
  nnoremap <silent> <Leader>fh :<C-u>Clap history<CR>
  nnoremap <silent> <Leader>ff :<C-u>Clap files ++finder=rg --ignore --hidden --files<cr>
  nnoremap <silent> <Leader>tc :<C-u>Clap colors<CR>
  nnoremap <silent> <Leader>fa :<C-u>Clap grep2<CR>
  nnoremap <silent> <Leader>fb :<C-u>Clap marks<CR>

  let g:dashboard_custom_shortcut={
    \ 'last_session' : 'SPC s l',
    \ 'find_history' : 'SPC f h',
    \ 'find_file' : 'SPC f f',
    \ 'change_colorscheme' : 'SPC t c',
    \ 'find_word' : 'SPC f a',
    \ 'book_marks' : 'SPC f b',
    \ }

  ```

- dashboard-nvim with fzf.vim

  ```viml
  Plug 'hardcoreplayers/dashboard-nvim'
  Plug 'junegunn/fzf.vim'

  let g:mapleader="\<Space>"
  nmap <Leader>ss :<C-u>SessionSave<CR>
  nmap <Leader>sl :<C-u>SessionLoad<CR>
  nnoremap <silent> <Leader>fh :History<CR>
  nnoremap <silent> <Leader>ff :Files<CR>
  nnoremap <silent> <Leader>tc :Colors<CR>
  nnoremap <silent> <Leader>fa :Rg<CR>
  nnoremap <silent> <Leader>fb :Marks<CR>

  let g:dashboard_custom_shortcut={
    \ 'last_session'       : 'SPC s l',
    \ 'find_history'       : 'SPC f h',
    \ 'find_file'          : 'SPC f f',
    \ 'change_colorscheme' : 'SPC t c',
    \ 'find_word'          : 'SPC f a',
    \ 'book_marks'         : 'SPC f b',
    \ }
  ```

## FAQ

- What is it different from vim-startify ?
  dashbaord is inspired by doom-emacs, startify provides a list of many files,
  Mru oldfile, etc., but do we really need this list, we will only open one file,
  and the file list takes up a lot of space, the dashboard uses fuzzy search plugin
  pop-up menu, it saves a lot of space, and provides more functions.

## Donate

Do you like dashboard-nvim? [buy me a coffe](https://salt.bountysource.com/teams/thinkvim-taigacute)😘!

[![Support via PayPal](https://cdn.rawgit.com/twolfson/paypal-github-button/1.0.0/dist/button.svg)](https://www.paypal.me/bobbyhub)

| Wechat                                                                                                          | AliPay                                                                                                       |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| ![wechat](https://user-images.githubusercontent.com/41671631/84404718-c8312a00-ac39-11ea-90d7-ee679fbb3705.png) | ![ali](https://user-images.githubusercontent.com/41671631/84403276-1a714b80-ac38-11ea-8607-8492df84e516.png) |

## Acknowledgement

- Inspired by [doom emacs](https://github.com/hlissner/doom-emacs)

- [vim-startify](https://github.com/mhinz/vim-startify)

## LICENSE

- MIT
