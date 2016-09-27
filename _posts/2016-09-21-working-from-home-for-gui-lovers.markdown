---
layout: post
title: Remote Text Editing for GUI Lovers
date: '2016-09-20 23:43:46 -0400'
published: true
---

## WFH + Unison = Productivity

My remote Atom workflow is built atop Unison. Unison can continuously scan local and remote directories for differences. When a change is detected, Unison determines if conflicts are present and takes automatic action when possible.

Once Unison is set up, you can run a sync job in the background that will bring your remote files to your local system and automatically sync changes back as your make them. You get the full speed of your favorite local editor and the convenience of working from anywhere.

I set up a Unison sync job between the `development` folders on my work and home PC. Benefits of working on the local filesystem include. If you're not (yet) a full-time vim/emacs wizard and you need to work remotely on a large number of files, try out Unison!


## Before you Begin

Unison needs to be set up on each computer participating in the file transfer. You must have the same version of Unison on each host. Some distributions have a `unison` package available for download. In my case, the file-system monitoring portion of Unison was not included, so I opted to build from source.

## Building Unison from Source

The official build guide can be found [here](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#building).

#### Fedora 24 Dependencies
`dnf install @development-tools ocaml ocaml-camlp4-devel ctags ctags-etags`

#### Ubuntu 16.04 Dependencies
`apt install build-essential ocaml liblablgtk2-ocaml-dev ctags`

#### Download the Source Archive

You'll want to grab the latest Unison source package from [https://www.cis.upenn.edu/~bcpierce/unison/](https://www.cis.upenn.edu/~bcpierce/unison/). Download the source .tar.gz file to your system. At the time of this writing, the latest version was 2.48.4. I pulled the source down to each of my systems with `wget`.

#### Build Unison

Extract the contents of the source archive.

`tar zxvf unison-2.48.4.tar.gz`

`cd` into the extracted `src` directory, and run `make UISTYLE=text` to build Unison.

Verify that Unison built successfully by running `./unison -version` which should output `unison version 2.48.4` or whatever version you are building.

#### Copy Build Result to /usr/bin

While still in the `src` directory, copy the resulting files to somewhere on your path. In my case, I'll copy to /usr/bin. You may need to use `sudo`.

`cp {unison,unison-fsmonitor,fsmonitor.py} /usr/bin`

## Configuring Unison to Securely Sync Content

#### Increase Filesystem Watcher Count

If you're watching a directory containing lots of source code like I wanted to, the default `max_user_watches` value specified by `inotify` is unlikely to be sufficient. You will need to update the `max_user_watches` on each machine participating in the sync.

To begin, check the number of files contained within the directory you want to sync.

`find DIR_NAME -type f | wc -l`

Now, check the maximum number of files that can be watched.

`cat /proc/sys/fs/inotify/max_user_watches`

If you're anywhere near to hitting the limit, be sure to increase the number of watchers to accomodate the watching all of your files. I doubled the number of files in my directory (which contained about 100,000 files) to get my `max_user_watches` of 200,000.

Set the new `max_user_watches`.

`echo fs.inotify.max_user_watches=200000 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`

#### Configure Synced Directories

In order to let Unison know which directories to sync, create a sync profile with the local and remote paths specified. For more information on creating a sync profile, read the docs [here](http://www.cis.upenn.edu/~bcpierce/unison/download/releases/stable/unison-manual.html#profileegs).

Create a .prf file in the `~/.unison` folder called `sample-sync.prf` containing your sync profile.

I used something similar to the "Minimal Profile" from the Unison docs. One of my sync roots is configured as a local path, the other is configured as an SSH path into my remote machine.

Unison can ignored paths based on the profile provided. For example, I didn't need to sync the assets from the remote host every time they were moved around during a build, so I ignored that path to skip unneccesary network traffic.

#### Copy SSH Keys

If you haven't already copied your SSH keys to the remote host, be sure to do so before continuing.

`ssh-copy-id user@remote-host`

## Run the Sync
#### Start the Sync Job

To run Unison using the profile we've just created, run:

`unison sample-sync -auto -repeat watch -logfile /tmp/unison.log`

Where `sample-sync` is the name of the profile we created in the previous step. Notice that I included some extra command arguments to log output, automatically resolve some conflicts, repeatedly run, and watch the filesystem for changes on both sides.

I usually run Unison in a `tmux` session.


## Final Thoughts

Atom is my daily driver. I learned vim more in-depth shortly after joining Red Hat. It's fun to feel like a professional hacker and live in the terminal, but when you're juggling lots of files, a nice graphical text-editor such as Atom significantly lightens my mental workload. Text-editing politics aside, being able to stick to the tools you're most comfortable with while working remote is great for efficiency and sanity.
