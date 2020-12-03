---
layout: post
title: How I made my first Github page
subtitle: Descriptions of steps and resources I used
thumbnail-img: /assets/img/github_pages.jpg
share-img: /assets/img/github_pages.jpg
tags: [Github pages, Jekyll]
---

Every story starst with google search!
I did my search, checked courses, trials and errors, doing and deleting, and finally my efforts ended to a place I like to call it my Github page.

Since I am lazy and not a professional writer, I try to briefly mention the steps that worked for me and my resources in this journey.

1- First we need to know what is github pages. I have learnt that [Github pages](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages) is a place for blogging as well as show casing potfolios. And good news, it is free!
As soon as you learn about Github pages, the word [Jekyll](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/about-github-pages-and-jekyll) becomes familiar to you, which is a static site generator software with built-in support for GitHub Pages and a simplified build process. So next I had to learn more about Jekyll.

2- It is recommended to set up Jekyll on your own computer so you can edit and preview your site locally, and when ready, push those changes to your GitHub repo. Since I had now idea where to start, I looked for online-courses, and [this one](https://www.lynda.com/GitHub-tutorials/Learning-Static-Site-Building-Jekyll/761964-2.html) in linkedin learning gave me a feel of what path I will be in. I started to follow the course and made my first locally hosted website with Jekyll. Although this course gave me the general idea, I could not deloy my site on the github pages platform and it only gave me blank website. Step 3 describes how I fixed this problem. I found another great resource to learn about github pages by [Jonathan McGlone](http://jmcglone.com/guides/github-pages/). But be aware that this tutorial misses the part to show you how to do Jekyll site deployment on your local computer and is only useful if you want to do everything online on the github.

3- I found out that the online course I have been following was using Athena theme which is not compatible with github pages (I wasted good amount of time searching why my github page is blank however github has already sent me an email saying I am using Athena theme which is not compatible with the github pages ). At this point I also learnt that I can clone one of the available [repos](https://github.com/topics/jekyll-theme) that provide sample github pages with compatible theme. I made a new website using the repo from [Beautifull Jekyll theme](https://github.com/daattali/beautiful-jekyll) and it worked well when I tried it on my github page. However, the problem here was that it gave me error when deploying it on my local computer.

4- Again after few trials and search, I realized the repo I selected is not compatible with the Jekyll config on my local computer and it misses two RubyGems. This has been resolved by running follwong commands:
 ~~~
    gem install tzinfo
    gem install tzinfo-data
 ~~~
 In addition, I added two new lines as
 ~~~
    gem "tzinfo"
    gem "tzinfo-data"
 ~~~ 
 in my Gemfile. Next, I updated the _Gemfile.lock_ file with the latest version of tzinfo and tzinfo-data that I have installed ( you can check versions online [here](https://rubygems.org/search?utf8=%E2%9C%93&query=tzinfo)), as two new lines:
 ~~~
    tzinfo (2.0.3)
    concurrent-ruby (~> 1.0)
    tzinfo-data (1.2020.4)
    tzinfo (>= 1.0.0)
 ~~~

5- Finally I got my site up locally after running the command 
 ~~~
    bundle exec jekyll serve
 ~~~
 Voila! now you can go to the address where jekyll serves your website locally which by default is _http://127.0.0.1:4000_. Every update in your website is visible by refreshing this locall address except changes in the __config.yml_ file which needs you to stop the server by _ctrl c_.

6- After these steps you have a localy running website and if you have commited and pushed your changes to your github pages repos, your github page will also work. I will put the required git commands here using git command line (make sure you are in the directory where your jekyll website is built):
 ~~~
    $git init   #to start the empty repos in your local computer. this command you just run it once. but the following commands needed to be done every time you want to push changes from local repos to your github page repos
    $git remote add origin https://github.com/yourgithubyousername/yourgithubyousername.github.io.git   #adding the address of your github pages link as your remote repos. The address is always your github username following _.github.io.git_
    $git add --all   #to include all your file in the current directory in the local repos
    $git commit -m "Your commit comment goes here"   #commit your changes
    $git -u origin master   #to push the changes to the master branch in the github repos
 ~~~
 If all the steps have been completed successfully, your website is ready for public access under the link address _yourgithubusername.github.io_ .

Last tip for writing posts or pages, it is by far easier to write them in markdown language than HTML. I tried this short [tutorial on Markdown](https://www.markdowntutorial.com/) which gives you a good foundation.




