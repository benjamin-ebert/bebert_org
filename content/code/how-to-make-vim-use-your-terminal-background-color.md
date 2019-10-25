---
title: "How to Make Vim Use Your Terminal Background Color"
date: 2019-10-25T23:07:49+02:00
draft: true
tags: ["Vim"] 
---

The trick is to set no background color at all. In your ```.vimrc``` put this
under your ```colorscheme``` configuration:
```
hi NonText ctermbg=none	
hi Normal guibg=NONE ctermbg=NONE
hi LineNr ctermbg=NONE 
```

Close and reopen Vim. It wil now have a transparent background, which means it
has the same background color as your terminal.
