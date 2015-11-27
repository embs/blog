---
layout: post
title:  "From Octopress to Jekyll!"
date:   2015-11-26 21:54:00
categories: jekyll octopress blogging en git github
---
[Several months ago][firstoctopress] I was pretty amazed with the ability of
blogging through a static pages generator that was open source and had a nice
name: Octopress. Some time later I am still quite delighted with another
analogous tool that is also open source but has a less fancy name: Jekyll.

Jekyll is the foundation for Octopress and what made me change to it at first
was that [GitHub encourages it][ghpwithjekyll]. Such encouragement comes along
with the promise of painless integration with GitHub pages.

I've took an while without updating the Octopress blog and get back to the labor
seemed pretty tough -- since I wanted to spend no time with configuration nor
stuff like that. After acknowledging GitHub inclination to Jekyll I've also read
[a blog post comparing the two blogging tools][jekyllvsoctopress] and
[this entry in the Octopress blog][octopressblogpost] which is not that comforting.

So the choice was made. Time to move on and get the life going on again.

# Moving out

First thing was following up the step-by-step guide for deploying Jekyll with
GitHub pages provided by GitHub. Easy peasy.

It was sad to verify that my CNAME configuration messed with the CSS, which had
to be also statically provided. [Configuring the Jekyll options][jekyllconfig]
did the trick and style rules were finally working. I've had already suffered
a lot with that on Octopress and this suffering probably done my life easier nowadays.

Next thing was to import the old posts from the former Octopress blog. I was
annoyed by the fact that I couldn't find the markdown files anymore. The only thing
that occurred to me was that GitHub neglected the posts since they lived in a
folder named `_posts`. (I've imaginatively created this rule of GitHub behavior)

After coming and going around a lot and trying an [HTML to Markdown][html2md]
tool, I've finally rediscovered that there was a branch named `source` in the
Octopress repository -- and all the markdown stuff was still there!

Since I've used the same git repository to introduce the new Jekyll blog, the
rediscovering made me seek for and [find][gittip] one awesome git feature that
I wasn't aware of: checkout files from a different branch.

    $ git checkout source -- source/_posts

And my posts were mine again!

# Moreover

Another thing that impressed me is how seamlessly is the generation of HTML from
the markdown files. That is probably accomplished by the [github-pages gem][ghpgem]
but I haven't dived deep on it yet. Maybe another time.

[firstoctopress]: https://github.com/embs/embs-blog.github.io/commit/e2bc5b28d6e2d6059f1d9db4b8d39dfba9190797
[ghpwithjekyll]: https://help.github.com/articles/using-jekyll-with-pages/
[jekyllvsoctopress]: https://lauris.github.io/blogging/2014/08/16/jekyll-vs-octopress/
[octopressblogpost]: http://octopress.org/2015/01/15/octopress-3.0-is-coming/
[jekyllconfig]: https://github.com/embs/blog/commit/3e141990f4ae1ba63683830e2446b8ef99ca9409
[html2md]: https://domchristie.github.io/to-markdown/
[gittip]: http://nicolasgallagher.com/git-checkout-specific-files-from-another-branch/
[ghpgem]: https://github.com/embs/blog/commit/f496d33372a5ef0f5a9c10add69b2894f825c4d5#diff-8b7db4d5cc4b8f6dc8feb7030baa2478R3
