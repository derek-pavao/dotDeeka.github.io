---
layout: post
title: "Free Hosted Blog: Jekyll and Github Pages"
tags: [Jekyll]
image:
  feature: abstract-6.jpg
  credit: dargadegetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true
---
## The Ideal Free Blog for any Developer

I have often wanted to start blogging. I've been working building software for a couple
of years now and occasionally I come across topics, gotchas or other things in my professional life
that I thought would make a good blog post. The thing that keeps me from doing it is
the setup and maintenance of the blog itself.

I have worked with both Drupal and WordPress in my professional career and in my opinion,
both are complete overkill for what I want out of a blog. I want my blogging experience to
be nice and easy. I know myself well and I know if I have to work at blogging, one thing is
certain, I wont blog for long. I decided I needed to come up with a list of what I wanted
and didn't want out of a blogging platform.

#### Things I **DON't** want:
 - I **DON'T** want to have to deal with updating and installing plugins.
 - I **DON'T** want to have to update core when a new version is released.
 - I **DON'T** want to have to deal with uploading changes to a host with FTP,
 SCP, RSYNC or other programs.
 - I **DONT'T** want to need a full LAMP stack on my machine to change my blog.


#### Things I **DO** want:
 - I **DO** want something that has a decent templating engine.
 - I **DO** want a library of free templates to choose from, I'm likely to not
 want to customize my template right away :)
 - I **DO** want a platform with a plugin archetecture so I can write extensions
 for the platform if I cant find anything off the shelf to use.
 - I **DO** want to be able to write my blog posts in markdown.
 - I **DO** need syntax highlighting for code in my posts
 - Also, what would be nice is if the platform were not written in PHP. I dont have anything
 against PHP, but I don't find it fun to write and this is supposed to be fun.
 - And Lastly, it has to be easy.

<!--end-excerpt-->

### Analyzing My Options
---

#### [WordPress](https://wordpress.org) (PHP)
Looking at the lists of wants and don't wants I began to search the web for options.
I actually began my search looking at WordPress. WordPress has become the defacto
in blogging software so I felt it deserved its fair shake. I quickly found plugins
to handle two of my items on the DO list: [WP-Markdown](https://wordpress.org/plugins/wp-markdown/)
to add markdown syntax to my posts, and [SyntaxHighlighter Evolved](https://wordpress.org/plugins/syntaxhighlighter/)
to add code highlighting to posts. But alas, I still was left with all the overhead of WordPress.
At this point I was sure I could get everything on my DO list with WordPress, but I decided to
continue my search for the perfect solution.

#### [KeystoneJS](http://keystonejs.com/) and [Calipso](http://calip.so/) (NodeJS)
I have been doing a lot of NodeJS development in my personal projects and spend my days
writing AngularJS code for a web client so naturally I wanted to look into my options from the
NodeJS community. The two projects I came across are [KeystonJS](http://keystonejs.com/) and
[Calispo](http://calip.so/). They are both built ontop of technoligies such as NodeJS, Express,
and MongoDB. These projects sound interesting but I dont think they satisfy my requirement of being easy.
I feel like, with either of these projects, I would spend more time playing with the tech than actually blogging,
they are just too bleeding edge tech for what I'm looking for.

#### [Frozen-Flask](http://pythonhosted.org/Frozen-Flask/) (Python)
A friend of mine at work mentioned to me how he had set up a blog with [Frozen-Flask](http://pythonhosted.org/Frozen-Flask/)
and was hosting it in an AmazonS3 Bucket for just a few cents a month. This sounded very interesting
to me. Flask is a very nice RESTful micro framework I had used a bit before. It is written in Python
and is very easy to use. The Frozen part of the name comes from the fact that this project
builds your Flask application into a set of static files that you can host on any traditional web server,
sounds interesting right? This is an example of using Frozen-Flask to build a static blog by [Florapdx](https://github.com/florapdx/My-Blog)
on Github.

#### [Jekyll](http://jekyllrb.com/) (Ruby)
Through all this research it seemed like building a static blog with Frozen-Flask was the solution I would
go with. I had heard a while back about hosting static sites on github with [GitHub Pages](https://pages.github.com/), either
using a specific repository name, or a gh-pages branch on a repo. This was even better in my opinion than
my co-workers solution of using AmazonS3, GitHub Pages is free! When I began investigating how GitHub pages works
I quickly came across Jekyll. Jekyll is a static site generator. It is just a Ruby Gem, comes with its own development server,
posts are written in either MarkDown or Textile, has a templating engine using Liquid, has a fair amount of free
themes, and the kicker... if you push a Jekyll site to a GitHub Pages repo it will generate the static site for you and
make it available at your domain.

At this point I was completely sold Jekyll and GitHub Pages are the answer. I can now manage and deploy my blog,
with only Git, and GitHub. I even get to write my blog posts in my beloved text editor Emacs.

### Installing and Configuring Jekyll on OSX
---

{% highlight bash %}
# Install the jekyll gem
$: [sudo] gem install jekyll

# Generate a new blog using the jekyll command
$: jekyll new jekyll-blog # jekyll-blog is the name of the
                          # directory that will hold your blog

# Start the development server so it will rebuild the blog
# when the files change
$: jekyll serve --watch

# By default your server should be available at localhost:4000
{% endhighlight %}


At this point you have a very basic Jekyll blog running. There
are some configuration settings stored in _config.yml. Things like
the title of the blog, your email etc. (NOTE: changes to your _config.yml file
do not take affect with out restarting the server. This is true regardless
of whether you used the --watch flag or not)

Posts are stored in the _posts directory. The post file names
take the form of YYYY-MM-DD-name-of-blog-post.md. Files that start with
a date are assumed to be published, those without are assumed to be drafts.

There are available free themes for Jekyll sites,
[jekyllthemes.org](http://http://jekyllthemes.org/).
Usually these themes will have instructions on how to use them with both
an existing site, and when starting a new site. I suggest if you plan
to use a free theme you choose it first and follow the instuctions
for using that theme for a new Jekyll site.

[Incorporated](http://incorporated.sendtoinc.com/) is a particularly nice theme.

### The Basics of Jekyll
---
Some basic things to know are...

Posts are just Markdown files. Published posts are always located in the _posts
directory and named YYYY-MM-DD-post-name.md. Unpublished posts dont have the date
bit, they are just post-name.md.

To serve drafts during development put them in a directory called _drafts and
start the development server with the --drafts flag
{% highlight bash %}
$: jekyll server --watch --drafts
{% endhighlight %}
All drafts will be served as if they're published, using the files last modifed
date as the published date

Posts contain a bit of YAML at the top of the .md file called FrontMatter.
FrontMatter defines some meta data about the post an example would be
{% highlight yaml %}
---
layout: post
title: My Awesome Post
---
{% endhighlight %}

Check out the [Jekyll Docs](http://jekyllrb.com/docs/home/) for a detailed
explanation of all the features of Jekyll.

### The Basics of GitHub Pages
---
There are two major types of GitHub Pages. There are User or Organization level
sites, and there are Project level sites.

User or Organization level sites are repositories where the name of the repository
is in the format <username>.github.io where <username> matches exactly your
GitHub username. When you push a Jekyll site to the master branch of this repo it will
be available at <username>.github.io. Take this site for example I have a repo in my acount
called dotDeeka.github.io, and it is available at http://dotDeeka.github.io

Project level sites are a little different. They live in the same repo as the project
they are for. Take the famous [Underscore.js](https://underscorejs.org) library.
The UnderscoreJS project on GitHub has a gh-pages branch with a static site in it.
If you navigate to [https://jashkenas.github.io/underscore](https://jashkenas.github.io/underscore)
you'll notice the documentation site is available there also.

For full docs, and a much better decription, on GitHub Pages check out
[https://pages.github.com/](https://pages.github.com/)

### In Conclusion
---
Jekyll is amazingly simple to use, at least for a developer type or someone tech savy.
It does require a bit of knowledge of the command line, installing Ruby Gems and running commands
and such. But, if your at least a little comfortable with that stuff, writing posts and managing
your blog is incredibly simple.
