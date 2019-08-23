---
title: "How to Serve Laravel Projects With Valet"
date: 2019-07-28T16:27:53+02:00
draft: true
---

* install valet
* cd into project root dir
* ```valet link```
* visit project-dir-name.test
* if it says 'It works!' but does not show the default laravel homepage, then
  the site is still being served by apache, not by nginx
* ```sudo apachectl stop```
* ```valet restart```
