# Monitoring Async Tasks and Notifications in Tmux

I wanted a workflow where I could run asynchronous tasks inside tmux panes or windows, switch to other work, and then get notified when the task was done or waiting on input from me.

This is similar to the workflow that agentic coding tools make possible: more task switching, more parallel work, and more long-running background tasks across one or more projects. The goal was not just to support coding agents, but also normal terminal work like builds, tests, or other commands that I want to revisit only when they need attention.

## Why the built-in tmux alerts were not enough

tmux has three built-in alert types:

- Bell
- Activity
- Silence

Those alerts are window-level and do not seem expressive enough for richer notification logic. They may support a simple or naive notification layer, but they do not give much control over interpreting pane output or distinguishing between different kinds of task state.

## Control mode seemed like the more general solution

My first implementation attempt used a tmux control mode client.

The idea was to monitor pane output directly and build notifications on top of that output rather than relying on tmux's built-in alerts. That would make it possible to react to richer signals, for example:

- OSC 9 notifications
- Other OSC sequences
- Arbitrary output patterns that indicate completion or blocked input

This seemed more general and more extensible than the built-in alert system.

## Where this broke down

The main problem is that a control mode client can only observe changes within one tmux session.

Because I use multiple tmux sessions, usually one per project, that means I would need one observer client per session. In practice, that turns into a fan-out model where multiple control mode clients are continuously watching pane output across sessions.

That ended up not being viable.

tmux buffers output per control mode client, which means this design can create a lot of copying. If the client does not read buffered output fast enough, the buffering can grow and cause instability. I was not able to fully isolate the exact failure mode, but my implementation of per-session observer clients eventually crashed the tmux server.

## Takeaway

The important thing I learned is that tmux control mode is probably the wrong primitive for broad multi-session observation of pane output.

Even though it is much more flexible than bell, activity, and silence alerts, the session-scoped client model and per-client buffering make it risky for this kind of always-on monitoring approach.

If I revisit this, it may be worth starting with the simpler tmux alert mechanisms first, even if they are limited, before trying to build a more general observer layer on top of control mode.
