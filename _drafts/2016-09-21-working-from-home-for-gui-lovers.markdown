---
layout: post
title: "Text-Editing on a Remote Machine for GUI Lovers"
date: "2016-09-20 23:43:46 -0400"
---

<!-- Insert image of Unison or Atom -->

As a software developer at a Linux company, I've learned that terminal-fu is, to a great degree, the measure of a man. I learned vim more in-depth shortly after joining Red Hat. It's fun to feel like a professional hacker and stay in the command-line all day, but when you're juggling twenty open files and a deadline, a nice graphical text-editor such as Atom can significantly lighten your mental workload. Being able to stick to whatever editor you're comfortable with while working remote is great for efficiency and sanity.

Before moving on, I should clarify that if you can just check your project into version control and then check it out remotely for editing, this post is not going to be at all useful to you. My situation is as follows: I have a massively powerful workstation containing my entire development environment which is parked at the office and powered on 24/7. Sure, I could perform edits locally, `git push` to a private branch, and `git pull` down to the office workstation for testing, but that would slow down my workflow immensely.

I've recently found a new remote workflow that has allowed me to return to using Atom locally (or any text editor) to make changes to projects on a remote filesystem at high speed, and I love using it.

So how do we work remotely in Atom? For starters, don't use the remote-atom package if you're working with an entire project (e.g. a web app contained within a directory). The remote-atom package allows for remote editing of files via SFTP 'checkout', but requires manual traversal of the remote host to open said files. Losing ctrl+p, the project tree, git tracking support, and project search capability mean that Atom becomes mostly useless next to vim over SSH in a remote situation.

My remote Atom workflow is built atop Unison. Unison (`unison` in the terminal) can continuously scan local and remote directories for differences. When a change is detected, Unison intelligently determines what action to take and then efficiently carries out any necessary networked file transfers.

Once Unison is set up, you can run a sync job in the background that will bring your remote files to your local system and automatically sync changes back as your make them. You get the full speed of your favorite local editor with all the convenience of working from anywhere with a solid internet connection. I haven't tested it elsewhere, but when I'm at my apartment
