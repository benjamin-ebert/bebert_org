---
title: "Best Unknown Vim Commands"
date: 2019-09-08T08:34:49+02:00
draft: false
toc: true
tags: ["Vim"] 
---

## `gq` - Autoformatting
`gq` autoformats your selection according to your formatting configurations in
`.vimrc`. I often use this after editing a paragraph when the formatting is
messed up. Jump to the beginning of the paragraph, hit `v` to switch to visual
mode, select the entire paragraph and hit `gq` - boom, the entire thing looks nice
again. Even faster: When you're at the beginning of the paragraph, hit `gq` in
normal mode, then hit `}` to auto format the whole paragraph.

## 2. :find and :tabfind
In your .vimrc ```set path=.,/usr/include,,**``` will make :find search
recursively from your working directory. You don't need to type the full file
name - hit Tab while you type to cycle through possible results. Using :tabfind
instead of :find will open the file in a new tab.

## 3. (), [] and {}
In normal mode hit [[ to jump to the beginning of a file and ]] to jump to the
end. That's faster than using gg and G. Hit { or } to jump between paragraphs.
If you're editing text, hitting ( and ) in normal mode is a convenient way to
navigate between sentences.

## 4. :e.
Opens the default vim explorer and shows the contents of your current working
directory. You can search, navigate and edit like normal text, hitting Enter
folds and unfolds directories. Pro tip: place your cursor on the file you want
to edit and hit t to open it in a new tab.

## 5. o and O
Hitting o in normal mode creates a new line below the line you're currently in.
The small one places the cursor in the new line, the big one leaves it where it
is.

## 6. :vs
This is best cobined with ```set splitright``` in your .vimrc to make the new
split open up on the right side of the current one.
