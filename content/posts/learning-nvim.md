---
title: "First 4 hours of using Neovim"
date: 2023-11-23
description: "Notes from what I've learned researching and using `neovim` for the past 4 hours."
---

I've finally decided to give scary Vim a try after I followed a few commands online and got stuck in it 2 years ago. After hacking at it for the past 4 hours, here are some short notes from what I've learned researching and using `neovim`.

### What is Vim?
In simple words, a text editor which considers the use of mouse to navigate/edit a blasphemy.  
Vim is a modal text editor (it uses different modes in which text can be manipulated). It is powerful and highly configurable. I've started getting my hands dirty with Neovim, which is an extensible fork of Vim through the use of highly functional plugins and comes with a better set of defaults like LSP, to support coding right out of the box.  

### Approach
As suggested by neovim itself, I went through the `:Tutor` which took me around 30-45 minutes. After that, I've spent the time up till now googling every little thing, from shortcuts, plugins, `init.vim`s et cetera.

### So far
Writing this article using Neovim, I've already used a few shortcuts to edit the title and metadata description.

1. Deleted previous title from the first apostrophe till the end of the line using `d$` which is the DELETE operator followed by the `$` motion which stands for 'end of line'.

2. I had to add the second apostrophe again which was removed by the `d$` command, so I looked for a way to delete the line excluding the second apostrophe. A kind lad had asked the same question on Stack Overflow 11 years ago.
I had to delete using the `dt'` command which stands for DELETE TILL <specified delimiter>. I'm already loving Neovim.

3. A simple copy of the first line of the post using `y` (YANK) and `p` (PUT) to paste it into the description section.

### What's new to me
* Neovim's document traversing capability is insane. It need less than 5 strokes of my keyboard to reach anywhere in the file. Capital G sends me to the end of the document. `gg` sends me to the first line. Any number followed by `G` sends me the specified line.  
* I can skip words using `w` and `e`, move to the end of the line using `$`, to the beginning of the line using `0`.  
* I can delete a number of words with the `d<number>w` command, starting from the cursor position.  
* I can skip to the next instance of a character using `f<char>`.
* Regardless of cursor position on a line, I can use `o` to start writing on a new line.
and so much more.

### New finding
While looking at a few basic Neovim configs, I ran into dotfile management which I think is super cool.
Took me no time to get invested in [dotbot](https://github.com/anishathalye/dotbot) to manage and backup my dotfiles, given how frequently I hop distros (my `.zshrc` is super close to my heart).

### Concluding remarks
It hasn't been even a day since I've been using Neovim and I already understand its hype. My speed of writing has taken a hit for now since I find myself trying to recall the commands. Sometimes forcing myself to use a Neovim shortcut instead of just going into 'Insert mode' and navigating with my cursor. As suggested by devs all around, I have my fingers crossed, learning Vim the hard way, hoping for the efforts to eventually pay off.
