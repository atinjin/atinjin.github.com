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

http://www.vimawesome.com
