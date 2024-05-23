---
title: "srcdit"
date: 2024-02-06
description: "Edit and source dotfiles directly from the terminal"
---

There was a phase when I was editing my `.bashrc` and `.zshrc` a lot. Having to edit them and then source them again and again soon became torturous. It would have been so much better if I had a tool to edit and source the files in just one step.  

The best part about being someone who works with and understands software is that I can build a tool to meet this requirement myself.
I worked on [srcdit](https://pypi.org/project/srcdit/) for a few days before getting busy with my internship, and I'm glad to announce that it's in a half-working condition. Check it out [here](https://pypi.org/project/srcdit/).  

It's (for now) a PyPi package and meant to be installed globally through pip.

### Usage

```bash
srcdit [filename] [key=value]
```

### How it works

srcdit runs a simple Python script (as of first week of Feb 2024 (I have other plans in mind)) to edit the key-value pair in the file for which the command has been invoked.  
If it does not find the given key in the file, it asks if the user would like to create a new field for the key.  
{{<figure class="center-image" src="https://github.com/osPrims/chatApp/assets/70942982/75eeec3d-cacd-48be-b9ff-57ff7e8e42bf">}}
<br>

The Python script then runs a bash script to `source` the file and bring changes into the env.  
But this is where we run into problems.

### The catch

The `source` is where I am currently running into a major problem.  

The app
* finds the key value pair
* edits it, if found (adds/skips if not found)

it even sources the edited file, but the changes do not persist in the shell. An `os.getenv(key)` inside the script outputs the modified value of the sourced environment variable but running an `echo $key` returns the previous value.

It took me 3 days to debug and find out why the changes weren't persisting in my terminal. I tried all combinations of `source`ing the file from the script, running a bash script to source the file, making the bash script call another bash script to source the file but none of it worked. The modified value showed up during application runtime but vanished as soon as my program exited, even though the key-value modification persisted in the file.  

### What was going on

Apparently, when a Python script runs, it runs in a subprocess inside the current shell. It's a child process of the shell which executes it. So when the Python script sources a file it modifies its own environment and, by rule, cannot modify the environment for its parent process.  

And since `source` is a built-in BASH command, it gets to modify the environment when invoked directly, instead of from a script.  

This has been the `source` of my headache since the past few days (sorry, couldn't help it).

### Possible workaround

To experiment with possible workarounds, I created a bash script to source a file. Even that did not bring environment variables into my current shell. What FINALLY worked was sourcing the bash script itself.

```bash
source srcdit.sh
```
This modified the current environment to retain the key-value pairs from a file.  

This also means that running my Python script as the entry point to the application will not work to create persisting changes in the current shell.

### [Rubber ducking](https://rubberduckdebugging.com/)

The only possible workaround I have come up with right now is sourcing the bash script to modify the current environment. A PyPi package is out of question if a full implementation of the edit + source is required. Creating an alias for `source script.sh [filename] [key=value]` will get the job done. I look forward to getting the app up and running with this approach soon so it can be packaged and published to software repositories - apt, pacman and dnf so that it helps a fellow shell customization enthusiast out there somewhere as well!