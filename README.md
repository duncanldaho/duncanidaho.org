[Untitled static site generator](https://notabug.org/untitled/untitled)
==============================

*Multi-site* static site generator! Written in Bash, uses Pandoc to convert
Markdown files into HTML pages.

Introduction
------------

You can download the latest version of Untitled here:\
<https://untitled.vimuser.org/>

For documentation, please also refer to the above website URL. This README is
merely an introductory text, *based on* the homepage of the above website.

Untitled is a static site generator. It is written in Bash, and it runs
pandoc to generate HTML pages. It is a *multi-site* static site generator.
It is intended for simple websites, particularly Free Software projects that
want a full website but don't want to bother with more complicated web based
publishing systems, or who don't want to mess around with HTML.

You write pages in Markdown, as `md` files. The variant of markdown is the
Pandoc variant, which you can read about here:\
<https://pandoc.org/MANUAL.html>

Pandoc can convert between *many* formats, but Untitled only supports converting
from Markdown into HTML. It is written precisely and exclusively with the goal
of making it easier for Free Software projects to create their own websites.
This is to fight against the trend of crappy github-powered websites that
plague the internet. It is highly desirable to see a return to the days where
software projects have websites!

History
-------

This software is very new, so expect some rough edges, and funky looking
websites! Here are some websites that already are built using `untitled`:

* <https://untitled.vimuser.org/> (official homepage of the untitled static
  site generator!)
* <https://libreboot.org/>

Actually, it's not new at all. This static site generator was originally
written for the [Libreboot project website](https://libreboot.org/) in 2017,
but it was *much* simpler and even more broken than the version you're now
reading about. That (very simple) generator was forked many times, across
different websites, with different features added.

The *untitled* static site generator was created to combine the features of
all the forks. Untitled static site generator was created by Leah Rowe, who
also leads the Libreboot project. Untitled is heavily based on the original
static site generator written by Alyssa Rosenzweig for the Libreboot website.

Untitled is *Free Software*. See the COPYING file included with
the *untitled static site generator*. Learn more about Free Software:\
<https://www.gnu.org/philosophy/free-sw.html> (basically, it means that *you*
have control over your own copy, to do whatever you want with, and you could
even fork it to make your own version if you wished)

-------------------------------------------------------------------------------

This README file is released under the terms of the GNU Free Documentation
License, version 1.3, as published by the Free Software Foundation with no
Invariant sections, no Back Cover texts and no Front Cover texts. You can find
this license here:
<https://www.gnu.org/licenses/fdl-1.3.en.html>
