---
layout: post
title: How I made my first Github page
subtitle: Descriptions of steps and resources I uses
cover-img: /assets/img/github_pages.jpg
thumbnail-img: /assets/img/github_pages.jpg
#share-img: /assets/img/path.jpg
tags: [github pages]
---

Every story starst with google search!
I did my serach, checked courses, trial and error, doing and deleting, and finally my efforts ended to a place I like to call it my Github page.

Since I am lazy and not a particular fan of writing novel! I try to briefly mention the steps that worked for me and my resources in this journey.

* 1- First we need to know what is github pages. Start with reading [About Github Pages](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages). Here I learnt that Github pages is a place for me to blog as well as show case my experiemts. And good news, it is free! As soon as you learn about Github pages, the work [Jekull](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages-and-jekyll) becomes familiar to you, which is a static site generator with built-in support for GitHub Pages and a simplified build process. So next I had to learn more about Jekyll.

* 2- I had no idea what is it all about, so started to for online-courses, and [this one](https://www.lynda.com/GitHub-tutorials/Learning-Static-Site-Building-Jekyll/761964-2.html) in linkedin learning gave me a feel of what my path I will be in. I started to follow the course and made my first locally hosted website with Jekyll. Although this course gave me thegeneral idea, I could not deloy my site on the github pages platform and it only gave me blank website.

* 3- I found out that that online course was using Athena theme which is not compatible with github pages (I waisted good amount of time searching why my github page is blanck however github has laready sent me an email to me saying I am using Athena theme which is not compatible with the github pages ). At this point I also learnt that I can clone one of the available [repos](https://github.com/topics/jekyll-theme) that provide sample github pages with compatible theme. I selected [Beautifull Jekyll](https://github.com/daattali/beautiful-jekyll) and it worked when I tried it on my github page. However, the problem here was that I could not deploy it on my local computer.

* 4- Again after sme trial and search, I realized the repos I selected is not compatible with the Jekyll config on my local computer. This has been resolved by:
~~~
gem install tzinfo
gem install tzinfo-data
~~~
and then in my Gemfile, i added:

* 5- It is by far easier to write posts and pages in markdown language than HTML. I tried this short [tutorial on Markdown](https://www.markdowntutorial.com/).



