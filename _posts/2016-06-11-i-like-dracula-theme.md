---
layout: post
title: I Like Dracula Theme.
modified:
categories: blog
excerpt:
tags: []
image:
  feature:
date: 2016-06-11T11:09:56+09:00
---

I like 'Dracula Theme'. So I will show you the way converting to Dark Theme at Mac OSX.

# Terminal

## Theme
It is easy to change the theme of mac Terminal.app. You can just choose the theme at the menu 'Preference'.

- Download the Dracula theme.
  - After finishing download you can see the folder contains 'Dracula.terminal' file.

~~~
git clone https://github.com/dracula/terminal.app.git
~~~

<figure class="half">
    <img src="http://blog.ryanjin.net/images/terminal_setting.png">
    <figcaption>Preferences of Terminal</figcaption>
</figure>

- Menu > 'Preferences'
- Click the Wheel icon
- Choose the 'import'
- Find the 'Dracula.teminal' file
- Click the 'default'
- Restart

## Prompt
- Open & Edit your profile file.

~~~
$ vim ~/.bash_profile
~~~ 

- Add the line. If you want to change the color or add unicode, you can do whatever you want.
  - You can find how to modify the linux prompt easily.
  - Briefly, "0;36" means Color of cyan and "\h" means host name. "\W" means current directory name.
 
~~~
export PS1="⌦ \e[0;36m\h\e[m@\W\e[0;36m$\e[m"
~~~

## Result
You can see the Dracula Terminal, now.

<figure class="half">
    <img src="/images/terminal_dark.png">
    <figcaption>Mac OS Dracula Terminal</figcaption>
</figure>

------

# Vim

Vim has many plugins for editing and coding. This web site instroduce you most of plugins.

[vim-awesome](http://www.vimawesome.com)

Here is the steps apply vim-plugins.
- find and edit the *.vimrc* file.
  - path : ~/.vimrc
- add the follow script first.

~~~
call plug#begin('~/.vim/plugged')

    " Make sure you use single quotes

    " Shorthand notation; fetches https://github.com/junegunn/vim-easy-align
    Plug 'junegunn/vim-easy-align'

    " Any valid git URL is allowed
    Plug 'https://github.com/junegunn/vim-github-dashboard.git'

    " Group dependencies, vim-snippets depends on ultisnips
    "Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'

    " On-demand loading
    Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
    Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

    " Using a non-master branch
    "Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }

    " Using a tagged release; wildcard allowed (requires git 1.9.2 or above)
    Plug 'fatih/vim-go', { 'tag': '*' }

    " Plugin options
    Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }

    " Plugin outside ~/.vim/plugged with post-update hook
    Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }

    " Unmanaged plugin (manually installed and updated)
    Plug '~/my-prototype-plugin'

    "Distraction-free writing
    Plug 'junegunn/goyo.vim'
    Plug 'valloric/youcompleteme'
    Plug 'vim-airline/vim-airline'
    Plug 'vim-airline/vim-airline-themes'
    
    "Plug 'dracula/vim'
    Plug 'zenorocha/dracula-theme'
    Plug 'craigemery/vim-autotag'
    " Add plugins to &runtimepath
call plug#end()
~~~

- restart the vim editor

Now you can see the 'Dracula Theme Vim'

<figure>
    <img src="/images/vim_dark_theme.png" alt="vim Dracula Theme">
    <figcaption>Dracula theme Vim</figcaption>
</figure>
