+++
title = "Wiki Using Hugo"
description = "Proposing a way to implement a public wiki using Hugo as a CMS"
date = 2022-06-12T23:53:31+05:30
author = "Rajat Arora"
categories = ["wiki"]
tags = ["organization", "pkm", "idea"]
draft: true

+++

You know what, I think there is a way to implement a Wiki-style website just by using Hugo. The workflow will be slightly different than [Obsidian](https://obsidian.md/) or [Roam](https://roamresearch.com/), but I think it _just_ might be possible.

Any Wiki operates by holding a bunch of information on different pages and then crosslinking them to create networked thought. Hugo:

- Already supports crosslinking using `ref` and `relref` [shortcodes](https://gohugo.io/content-management/cross-references/). The syntax is a little different than wikilinks: `{{< ref "page" >}}` as opposed to `[[page]]`, but it can be managed using clever keyboard shortcuts.
- Can theoretically support [transclusion](https://en.wikipedia.org/wiki/Transclusion) by some clever use of shortcodes. (It is a hypothesis at this point)

Furthermore, we can create a new [section](https://gohugo.io/content-management/sections/) specifically for wiki pages so that those can be logically separated from the rest of the site. Hugo already supports layouts at a section level so the content can be styled differently too.

