# How my site works

My site is built with a combination of [Jekyll](https://jekyllrb.com) and [GitHub Pages](https://guides.github.com/features/pages/) along with some other bits of code I’ve found around the interwebs.  I recently upgraded the theme and it stomped on a bunch of my configurations.  I didn't think to put it in git and my notes are terrible.

Here are some links and resources (and other tips) to remember how this all works next time I wait 2 years between blog posts.

### Basic Ingredients

* [Official Jekyll Docs](https://jekyllrb.com)
* [Getting started with Jekyll](https://jekyllcodex.org/getting-started/)
* [GitHub pages](https://pages.github.com)
* [Getting started](https://www.aleksandrhovhannisyan.com/blog/getting-started-with-jekyll-and-github-pages/#how-to-create-pages-in-jekyll) (and everything else) walkthrough

### Extras

* [Hydejack](https://hydejack.com) Jekyll theme I used
* [Hover.css](https://ianlunn.co.uk/articles/hover-css-tutorial-introduction) CSS to make links and buttons "hover"
* [Lightbox2](https://lokeshdhakar.com/projects/lightbox2/) CSS for photo galleries
* [Simple Search](https://github.com/christian-fei/Simple-Jekyll-Search) Search for Jekyll sites
* [Simple Search Tutorial](https://blog.webjeda.com/instant-jekyll-search/) Simple Search walkthrough

#### **Jekyll Tips**

* Start local server on localhost, port 4000

```
$ bundle exec jekyll serve
```

* Start local server on 0.0.0.0 so other hosts can connect/test

```
bundle exec jekyll serve --host=0.0.0.0
```

