---
layout: post
title: How to make a blog
subtitle: From creation to deployment
date: 2021-02-18 07:01 -0600
background: 'https:////images.unsplash.com/photo-1493217465235-252dd9c0d632?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80'
---
Blogs! They're a great way to showcase thoughts and ideas. I created this blog to create blogposts about my side-projects and hobbies.
I started by leafing through random github repos of software engineers and UX designers, until I found a theme that I liked. [StartBootstrap/startbootstrap-clean-blog-jekyll](https://www.google.com/search?client=firefox-b-1-d&q=StartBootstrap%2Fstartbootstrap-clean-blog-jekyll+) had everything I wanted- minimalist design, a backdrop image, and placement of posts on the front page. 
And then setup was pretty straightforward. 

#### I. Install Ruby and Jekyll
Ruby is a programming language, and jekyll is your trusty site generator that depends on Ruby to run. 
1. Install Ruby by following one of the suggestions in the [Ruby Installation Guidelines](https://www.ruby-lang.org/en/documentation/installation/). Check if it was installed by running 

    ```ruby -v``` 

    in your terminal/powershell/cmdline/etc.
2. Installing ruby should also install `gem`, which is both the term for libraries/pkgs used in Ruby, and is also the command you can use to manipulate RubyGems, which basically is another cmdline tool to manipulate gems. Check that gem was installed by running 

    ```gem -v```
3. Jekyll is a gem that will be the foundation for your blog. Install jekyll by running

    ```gem install jekyll bundler```
   
    <details>
    <summary>Common problem</summary>
       If you run into errors, prepare to spend some time fixing the dependencies between ruby, gem, and jekyll. For me, compilation was failing because there were two versions of ruby installed on my machine. The wrong one was being referenced each time I tried to compile. I changed the path of the ruby being called so that it led to the more recent version, and then deleted the old version of ruby, which fixed the problem.
    </details>

    Make sure you installed it by running `jekyll -v`.

#### II. Create a blog with Jekyll and deploy it locally.
1. You can create your own Jekyll blog by running

    ```jekyll new <blogName>```
    
    This blog will use the default Jekyll theme called `minima` but you can change the theme by replacing the theme in the `Gemfile` file. More to come on that.
2. Run 

    ```bundle exec jekyll serve``` 
    
    in your shell/cli/terminal/powershell, and go to the server address the build states (it'll probably be http://127.0.0.1:4000/)    and voila, you have your blog. 

#### III. Personalize your blog
If you choose to build your own blog with custom interactions and design, this section won't help you very much. 
1. If you decide to use a theme, go to your `Gemfile` which should've been automatically created when you first ran `jekyll new <blogname>`. The `Gemfile` maintains all the gems you need for your site to load properly. Not only will it include `jekyll` since your site needs Jekyll to run, but it will also include the default theme, `minima`. Replace it with the gem of a theme of your choice, and the website will render in that theme automatically. 
2. However, further personalization requires another step. It's likely that if you are using a theme from a gem, you won't be able to personalize it very much. Think of a gem, or any library or package as a building made out of legos. You can't just yank out a lego- it's built in. So in order to have more control and freedom over your blog, you're going to have to take the source code which open-source themes will offer, and refactor it. <br/>
    <details>
        <summary>Customization in this blog</summary>
        For myself, I didn't want the 'contact' tab. It was broken when I first deployed my blog locally, and for it to work, I needed to sign up to an email service. Having a broken feature on the UI seemed like a big flaw on my blog, so I decided to take it out. (I also wanted to change the font and some of the layout templates). <br/>
        So find out what files do what. What I did, was I found out that there were files that were specifically there to make the theme a gem, and files that actually made up the blog and its features. I just needed to keep the latter. 
        Another customization that a lot of people (myself included) like to do is on the css files. It's there you can control most of the visual aspects of your blog, such as font size and type, margin, kerning, etc. Most themes employ bootstrap which has its own css file that the build generates and uses. If you want to override this, [do not modify the bootstrap.css file, and instead, create your own css file and place it beneath the reference to the bootstrap.css file](https://stackoverflow.com/questions/8596794/customizing-bootstrap-css-template)
    </details>


#### IV. Deploy to github
1. Push your branch to github in a repo that is specifically named `<your-github-username>.github.io`. This is how Github will understand this is going to be your personal website and will render it as so. 
2. Wait a bit- grab some coffee or water, and then head over to `https:<your-github-username>.github.io`. You'll be able to see your neat new blog. (You also might get a nice email from github saying if it was a success or a failure.)

#### V. Writing posts
When you first create your site by running `jekyll new <blogname>`, you'll find that there will be a number of folders created with underscores in front of their names, like `_includes`, `_layouts`, and `_posts`. This folder structure is what jekyll needs to build your site. 
1. Create a test post to make sure things work. In the `_posts` folder, create a markdown file with the title formatted in `YYYY-MM-DD-title.markdown`. 
2. Jekyll takes markdown content and passes it through templates indicated in the YAML front-matter block at the top of each page. This specific page also has a front-matter block: 
```
---
layout: post
title: How to make a blog
subtitle: From creation to deployment
date: 2021-02-18 07:01 -0600
background: 'https:////images.unsplash.com/photo-1493217465235-252dd9c0d632?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1350&q=80'
---
```
The first line indicates to Jekyll that this page should be rendered as a post defined in the layouts, which is the folder houses all the templates. Add the front-matter block to the top of your file with the details about layout and title at the very minimum.
3. Run `jekyll serve`. You should see your post hosted as a static page in your blog.

And that's it 👏