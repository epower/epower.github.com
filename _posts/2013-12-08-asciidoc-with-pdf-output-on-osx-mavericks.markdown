---
title: Asciidoc with PDF output on OSX Mavericks
layout: post
---

I recently updated to OSX Mavericks on my work laptop. All seems well at the moment (nothing unfixable) but I was trying to get [asciidoc](http://www.methods.co.nz/asciidoc/) outputting PDFs as I did previously. As this was a relatively new machine, I hadn't fully install all my tools on it. 

A2x installed with no problems as part of the asciidoc bundle from Homebrew. But there was no dblatex and a few noted issues about [environment variables](https://github.com/akosmasoftware/eBook-Template/issues/1). 

So I found the necessary path information and added to my '.bash\_profile'.

    export TEXMFROOT=/usr/local/texlive/2013
    export PATH=/usr/texbin:$PATH

Then I used the 'easy\_install' package to get dblatex installed  (the pip package seems to have its own issues).


