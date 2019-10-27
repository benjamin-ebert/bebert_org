---
title: "Overlays"
date: 2019-10-27T15:04:06+01:00
draft: false
tags: ["CSS"] 
---

Suppose we have a html structure like this:

```
<div class="surrounding-element">
	<div class="regular-content">This is regular content</div>
	<div class="overlay">This is the overlay</div>
</div>
```

The core CSS-attributes are position and z-index:

```
.surrounding-element {
	position: relative;
}

.regular-content, overlay {
	position: absolute;
}

.overlay {
	z-index: 10;
}
```
