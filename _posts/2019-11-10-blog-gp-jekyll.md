---
layout: post
title:  "Blogging with Jekyll and Github Page"
date:   2019-11-10 10:32:46 +0800
categories: meta
---

I was using [Typlog](https://typlog.com/) as my blogging platform. It
has some nice themes and has been reliable for me for the last 2
years. However, earlier this month I have decided to move my blog to
[Github Pages](https://pages.github.com/), for three reasons:

1. It is free, whereas Typlog charges $5/month.
2. I want to be more active on Github, so I might as well move my blog
"closer" to it.
3. There are some nice org-mode to Jekyll workflows which allow me to
write in Org-mode and automate some of the publishing process.

Right now you are reading this page on Github Page. In this post, I
will describe the steps here. Hopefully it saves other people from
some confusion I had.

## Github Page

[Github Page](https://pages.github.com/) is a static site hosting
service provided by Github. Each Github user is entitled to a
`user.github.io` domain name, where `user` is the username on Github.

You can follow steps
[here](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site)
to set up an empty Github Page site, as well the local repository
corresponding to it. Note that at this point the site
is empty.

## Setting up Jekyll

[Jekyll](https://jekyllrb.com/) is a static site generator. Github
Page accept it as the content management backend for Github page. Before we
set up and Jekyll, we need to install `ruby` in our environment, since
Jekyll is actually a ruby package.

- Follow the steps [here](https://www.ruby-lang.org/en/documentation/installation/) to install ruby.

Our Jekyll site will be a ruby project, and `bundler` is tool popular
for managing dependencies for ruby project. I used it while setting up
this site.

- Follow the steps [here](https://bundler.io/) to install `bundler`

At this point one is ready to initialize the Jekyll backend.

{% highlight sh %}
$ cd user.github.io # change directory to the Github Page repo
$ bundle init     # create an empty Gemfile for bundler
{% endhighlight %}

To be able to use Jekyll, one needs specify the Jekyll dependencies in
the new Gemfile. I chose to use the pre-bundled `Github Pages` gem and
it worked for me. Read more about it
[here](https://github.com/github/pages-gem). Add the config to the new
Gemfile and run `bundle install`:

{% highlight sh %}
$ echo "gem 'github-pages', group: :jekyll_plugins" >> Gemfile
$ bundle install
{% endhighlight %}

This will install all dependencies specified in the Gemfile. We are
ready to initialize the Jekyll environment:

{% highlight sh %}
$ bundle exec jekyll new . --force
{% endhighlight %}

The official Github Pages [documentation](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site-with-jekyll) also recommends changing the
Gemfile after the above steps. Particularly, it recommends commenting
out the `Jekyll` dependency and uncommenting `github-pages` dependency:

- Comment out this line:

{% highlight ruby %}
gem "jekyll", "~> 3.8.5"
{% endhighlight %}

- Uncomment this line:

{% highlight ruby %}
gem "github-pages", group: :jekyll_plugins
{% endhighlight %}

- And change it to the following, where `VERSION` is the version
specified [here](https://pages.github.com/versions/):

{% highlight ruby %}
gem "github-pages","~> VERSION", group: :jekyll_plugins
{% endhighlight %}

Run the following command to see the Jekyll site spin to life.

{% highlight sh %}
$ bundle exec jekyll serve
{% endhighlight %}

Well not really. It will only start a local instance, allowing you
preview changes in real time before publishing online. You would need
to push the changes back to the Github remote branch in order for them
take effect for your site.

## Theme

The jekyll instance we just spinned came with the default theme. I
changed the theme to Yizheng's `moving` - something I saw on Hacker News and
quite like. You can find it
[here](https://github.com/huangyz0918/moving).

Changing the theme is pretty easy. As the author mentioned, all it
takes is changing `theme: xxx` to `remote_theme:
huangyz0918/moving` in the `_config.yml` file.

At this point, the blog is 90% ready. I took a look at Yizheng's
[blog](https://blog.huangyz.name/), and copy a few useful things, such
as adding the visitor counter and link to about page at the footer.

## Next

Next I want to explore the workflow for org-mode to Jekyll
publishing in emacs. 

Hope this is helpful for you and happy blogging!