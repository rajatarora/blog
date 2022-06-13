+++
title = "Wiki Using Hugo"
description = "Proposing a way to implement a public wiki using Hugo as a CMS"
date = 2022-06-13T13:15:08+05:30
author = "Rajat Arora"
categories = ["wiki"]
tags = ["organisation", "pkm", "idea"]
draft = true

+++

You know what, I think there is a way to implement a Wiki-style website just by using [Hugo](https://gohugo.io). The workflow will be slightly different than [Obsidian](https://obsidian.md/) or [Roam](https://roamresearch.com/), but I think it _just_ might be possible.

Any Wiki operates by holding a bunch of information on different pages and then crosslinking them to create networked thought. Hugo:

- Already supports crosslinking using `ref` and `relref` [shortcodes](https://gohugo.io/content-management/cross-references/). The syntax is a little different than wikilinks: `{{</* ref "page" */>}}` as opposed to `[[page]]`, but it can be managed using clever keyboard shortcuts.
- Can theoretically support [transclusion](https://en.wikipedia.org/wiki/Transclusion) by some clever use of shortcodes. (It is a hypothesis at this point)

Furthermore, we can create a new [section](https://gohugo.io/content-management/sections/) specifically for wiki pages so that those can be logically separated from the rest of the site. Hugo already supports layouts at a section level so that the content can be styled differently.

## Backlinks

Another feature that a wiki typically offers is a list of backlinks at the end of each page. E.g. If five different pages link to a page, those five are listed at the bottom of the page. Such a feature increases the discoverability of notes in a wiki.

Alas! Hugo doesn't offer such a feature out of the box. We will need to build it.

What Hugo _can_ do is to add an arbitrary number of `params` into its frontmatter. One person has [already implemented](https://gabrielleearnshaw.medium.com/implementing-backlinks-in-a-hugo-website-e548d3d8f0e0) a way to render backlinks into a Hugo template by leveraging the power of frontmatter parameters. However, his way of adding page details manually is very cumbersome. I'm thinking of something much more automated.

We've already established that we will be using the `ref` and `relref` shortcodes to manage internal links. What if we were to write a script that _preprocesses_ the markdown, _extracts_ all `ref` and `relref` shortcodes from it, and then adds all pages referenced in them into the YAML frontmatter parameters?

This could work!

## Block References

How about block references? Hugo already adds an `id` attribute to each heading element in the content. These can be used as-it-is in `ref` and `relref`. If headings can be considered _sections_ in a post, then we're good with _section-level references_ already. 

Will I require anything more granular? I don't think so. I'm not going to use this solution as an _infinite outliner_... just like a plain 'ol wiki :smile:.

## Zettel's

The idea behind a _Zettel_ is that it is a self-contained note that other Zettels can cross-reference. Zettel's with the same theme can be grouped to form a _hub_. 

Hugo already provides a way to group similar content &mdash; [taxonomies](https://gohugo.io/content-management/taxonomies/). We can create a new taxonomy for the Zettel grouping. It will not be applied to other parts of the blog so that the usual blog posts will remain oblivious to it. Inside a wiki, though, it will take on a life of its own.

## Related Content

Not just the backlinks, a wiki can also have other ways to specify similar content. E.g. content in the same category, with the same tags, in the same series, etc. We can create a _new_ partial that can surface such content and link it to the bottom of the page. MOAR discoverability FTW!

## tl;dr

- Hugo can be used to create a wiki-like site as it supports crosslinking and _theoretically_ supports transclusion.
- Backlinks implementation needs some sort of preprocessing of markdown text.
- Block references are not possible, but _Section_ references are.
- New taxonomy and clever usage of Hugo features can render a _related content_ section that can surface relatable content. 
- This is highly hypothetical, and a proof-of-concept implementation is the only way to determine if this can be done. (My gut instinct says yes).
