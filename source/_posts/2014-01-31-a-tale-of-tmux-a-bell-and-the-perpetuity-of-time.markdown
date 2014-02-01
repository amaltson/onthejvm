---
layout: post
title: "A tale of tmux, a bell and the perpetuity of time"
date: 2014-01-31 14:03
comments: true
published: false
categories: tmux
---

![perpetuity of time](http://upload.wikimedia.org/wikipedia/en/d/dd/The_Persistence_of_Memory.jpg)

I've been using [tmux](http://tmux.sourceforge.net/) for a while and love it.
I had heard of tmux on various podcasts and through Twitter, but I was finally
convinced to try it in early 2012 after listening to the [tmux episode on the Changelog](http://thechangelog.com/73/)
(excellent podcast by-the-way). [tmux: Productive Mouse-Free Development](http://pragprog.com/book/bhtmux/tmux),
which was the topic of the podcast, is an excellent book for getting started
with tmux. In the books short 88 pages it takes you from basics to advanced
features to kick start your tmux development.

After some experimentation, I got into a good workflow with tmux. I particularly
like using tmux with [tmuxinator](https://github.com/aziz/tmuxinator) to set up
projects and easily launch a full tmux environment with all my panes and windows
running the applications I configured in the tmuxinator YAML file.

As much as I loved tmux, one thing really bugged me. If I had several tmux
sessions open, which I was prone to do as I'd have several things on the go, the
terminal bell kept going off. It would go off regardless of whether something was
happening in that tmux session or not. I use iTerm and Growl, so bell events 
manifest themselves through Growl. This is actually surprisingly useful
because when I have a long running task in a tab I'm not looking at,
when the task completes and the shell becomes idle, I get a nice Growl alert.
Unfortunately, this feature is not so useful when it happens all the time and
nothing actually happens in the tab.

![tmux-bell](/images/tmux-bell.png)

I searched around extensively trying to figure out the issue thinking it
might be a tmux bug, or an iTerm bug. I came up with nothing, so I forgot about
it and just ignored the Growl notifications. Then, all the sudden, one day I
noticed that all the tabs ring their bell at the same time. Strange... what
could it be? And then I looked at the corner of my tmux window and there
was the answer.

![tmux-time](/images/tmux-time.png)

The corner of the tmux window holds the tmux status bar. As it turns out,
the default tmux configuration holds the date and **time**, in **minutes**.
Every minute, each tab that's running tmux updates to display the current time.
Time is ever perpetual, always marching forward, and always setting off bells in
tmux sessions.

The solution was easy enough, change the default status bar to only show the day
and month.

```
set -g status-right "#T %d %b"
```

![tmux-date-no-time](/images/tmux-date-no-time.png)

Voila! Now my bells and Growl notifications are useful again.
