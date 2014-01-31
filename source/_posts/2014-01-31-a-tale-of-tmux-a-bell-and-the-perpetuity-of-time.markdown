---
layout: post
title: "A tale of tmux, a bell and the perpetuity of time"
date: 2014-01-31 14:03
comments: true
categories: tmux
---

I've been using [tmux](http://tmux.sourceforge.net/) for a while and love it.
I had heard of tmux on various podcasts and through Twitter, but I was finally
convinced to try it in early 2012 after listening to the [tmux episode on the Changelog](http://thechangelog.com/73/)
(excellent podcast by-the-way). I went out and got the book that was the topic
of the podcast, [tmux: Productive Mouse-Free Development](http://pragprog.com/book/bhtmux/tmux).

After some experimentation, I got into a good workflow with tmux. I particularly
like using tmux with [tmuxinator](https://github.com/aziz/tmuxinator) to set up
projects and easily launch a full tmux environment with all my panes and windows
running the applications I configured in the tmuxinator YAML file.

As much as I loved tmux, one thing really bugged me. If I had several tmux
sessions open, which I was prone to do as I'd move from project to project, the
bell kept going off. When I say bell, I mean the terminal bell. It'd go off
regardless of whether something was happening in that tmux session. I use iTerm
and Growl, so bell events end up popping up through Growl. This is actually
super useful. When you have a long running task in a tab you're not looking at,
when the tab completes and becomes idle, I get a nice Growl alert. It's not so
useful when it happens all the time and nothing actually happens in the tab.

![tmux-bell](/images/tmux-bell.png)

I did a bunch of Googling trying to figure out why it was happening, thinking it
might be a tmux bug, or an iTerm bug. I came up with nothing, so I forgot about
it and just ignored the Growl notifications. Then, all the sudden, on day it
dawned on me. I looked at the corner of my tmux window and there was the answer.

The corner of the tmux window holds the tmux status bar. As it turns out,
the default tmux configuration holds the date and **time**, in **minutes**.
Every minute, each tab that's running tmux updates to display the current time.
Time keeps going forward and every minute I got an alert.

The solution was easy, change the default status bar to only show the day and
month.

```
set -g status-right "#T %d %b"
```

Voila! Now my bells and Growl notifications are useful again.
