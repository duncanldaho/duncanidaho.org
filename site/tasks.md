---
title: tasks
x-toc-enable: false
...

to do
----

NST gallery:

* bash script to iterate through image directory, needs to:
  1. Generate thumbnail using imagemagick
  2. append an html/md entry for lightbox gallery
  3. possibly organize them? use css for better grid?
* set up sud-domain for delivering images?

make about page for licenses, git repos, and about

go through source files and make sure all licenses are being properly credited

go through build script TODOs to see what can be done

continue to remove unnecessary/unused files

---

notes
----

Area under footer:

* Markdown link: comment out lines 458-459 in build script
* Site map: set SITEMAP_LINK="" in lang/en/strings.cfg
* untitled plug: set SHAMELESS_PLUG="" in lang/en/strings.cfg OR comment out line 473 in build script

---

done
----
Start with copy of www-example, alter the css, figure out how the build bash
script works.

Make page for neural style transfer gallery

Get rid of links below the footer, put them in footer?

Look into lightbox options. Ideally minimal html/css, absolutely no javascript
or php
