---
title: "On Official NUSNextBUS App"
date: 2023-05-16T22:45:22+08:00
draft: false
---

# Current Issues

## Ambiguous Logic

### Is Publicity a Top Priority?

The app prioritizes loading `/Publicity` over other content.
This causes a problem when the internet connection is unstable,
as users will see a large loading spinner on the screen.
Sometimes, the app will not load anything even if the connection comes back.
A better solution would be to load `/Publicity` lazily or asynchronously.

### Why Update the Bus Station List Every Time?

The app requests `/BusStops` every time it starts.
This is wasteful and inefficient,
as it rarely changes.
We could save the list in local cache
or even hard-code them into codebase.

### What Stops Bus Station List from Updating?

The app sorts the Bus Station List by distance when it starts.
However, if users switch to another app and come back later,
the list does not refresh and shows outdated information.
It would be helpful to have a button to manually update the list.
