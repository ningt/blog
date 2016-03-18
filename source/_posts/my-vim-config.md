title: my vim config
date: 2016-03-18 17:26:13
tags: vim
categories: vim
---
I have used sublime for the past three years of my university life, honestly speaking, it's pretty, fast and has many handy plugins. I also used vim to edit config files on server, you know, on the terminal, it just works out of box. Recently I decided to use vim for my project as well, and I wanna share my vim config. I will keep updating this.


```
syntax enable
set background=dark
colorscheme solarized

set tabstop=4     " number of visual spaces per TAB
set shiftwidth=4  " Indents will have a width of 4
set softtabstop=4 " number of spaces in tab when editing
set expandtab

set number
set showcmd
set cursorline
set wildmenu      " visual autocomplete for command menu
set showmatch     " highlight matching [{()}]

set incsearch
set hlsearch

fun! <SID>StripTrailingWhitespaces()
    let l = line(".")
    let c = col(".")
    %s/\s\+$//e
    call cursor(l, c)
endfun

autocmd BufWritePre * :call <SID>StripTrailingWhitespaces() " auto trailing whitespace

" move to beginning/end of line
nnoremap B ^
nnoremap E $

" set view window's center at current cursor
nnoremap j jzz
nnoremap k kzz

" jk is escape
inoremap jk <esc>

set nocompatible              " be iMproved, required
filetype off                  " required

```

I also use [Vundle](https://github.com/VundleVim/Vundle.vim) to manage plugins. There are a few plugins I found them are quite useful.

```
Plugin 'bling/vim-airline'
Plugin 'airblade/vim-gitgutter'
Plugin 'pangloss/vim-javascript'
Plugin 'kien/ctrlp.vim'
Plugin 'ervandew/supertab'
Plugin 'scrooloose/nerdtree'
Plugin 'terryma/vim-multiple-cursors'
```

For the compelte vim config, you can check my github repo [here](https://github.com/ningt/vimrc).