---
layout: post
title: Blogging on the road
tags:
- tech
- writing
published: true
---
Being [limited to 7kg of stuff][permalink-packing-list], I opted not to bring my laptop (1.82kg with case) and instead threw down the money to buy a tablet (800g with case and keyboard). But how would I publish any musings about my travels without a laptop? I knew I wanted to use [Github][github], but I wasn't sure how well it works with tablets.

<!--more-->

So after a bit of searching online and trial and error, I set up [Github Pages][github-pages] with [Jekyll][jekyll] from my laptop. ([This Github documentation][github-pages-with-jekyll] has more details about how to use the two of them together, and [this Smashing Magazine post][sm-build-a-blog] gives you a good starting point.)

What approaches did I try, and which did I ultimately go with?

1. [Working Copy][workingcopy] and [Git2Go][git2go] were the first iPad apps I came across, but both require upgrading to a premium level of service to actually push any changes to Github.
1. [CodeHub][codehub] seemed like an okay free version, but the interface is a bit lacking.
1. I found [Editorial][editorial] (pay $9.99 once and get it both on iPhone and iPad), which is a [Markdown][markdown] editor for iOS that supports workflows to automate repetitive tasks like interacting with Github. [This workflow][hardscrabble] does just that, and it was pretty simple to implement.
1. But in the end, it wasn't an app that I went with at all: [Prose][prose], which is a third-party web interface to edit Github files was the best option, and it was free. It has syntax highlighting, the ability to preview edits, and isn't limited to editing Markdown files: what more could I ask for?

In case you're interested, here's a [cheatsheet for Markdown syntax][md-cheatsheet].

[codehub]: http://codehub-app.com
[editorial]: http://omz-software.com/editorial
[git2go]: http://git2go.com/
[github]: https://www.github.com/
[github-pages]: https://pages.github.com/
[github-pages-with-jekyll]: https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/
[hardscrabble]: http://www.hardscrabble.net/2015/how-to-jekyll-from-ios
[jekyll]: https://jekyllrb.com/
[markdown]: http://whatismarkdown.com
[md-cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[permalink-packing-list]: /the-7kg-limited-packing-list
[prose]: http://prose.io/
[sm-build-a-blog]: https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/
[workingcopy]: http://workingcopyapp.com
