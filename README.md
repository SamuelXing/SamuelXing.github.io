<p align="center">
    <h2 align="center">This is my offical blog- <a href="http://zixing33.cc">Website</a> </h2>
</p>

<p align="center">
This blog is contructed by Jekyll and deployed on Github pages. The theme is developed by Sérgio Kopplin. Thanks Kopplin. If you are interested in constructing your own blog by using these tech stacks, you can follow the instructions as bellow to do so. The following steps are exactly how I build this blog. Enjoy.
</p>




## What has inside

- [Jekyll](https://jekyllrb.com/), [Sass](http://sass-lang.com/) ~[RSCSS](http://rscss.io/)~ and [SVG](https://www.w3.org/Graphics/SVG/)
- Tests with [Travis](https://travis-ci.org/)
- Google Speed: [98/100](https://developers.google.com/speed/pagespeed/insights/?url=http%3A%2F%2Fsergiokopplin.github.io%2Findigo%2F);
- No JS. :sunglasses:

## Setup

1. Download this [repo](https://github.com/SamuelXing/SamuelXing.github.io).

2. Setup local envrionment. (On Mac)
	- Ruby: I'm using v2.1.4. You can use [RVM](https://rvm.io/) to manage the different ruby versions on your local machine. You can see more details about how to use rvm for this project in <a href="<a href="README.md#Appendix">Appendix</a> section
	
	- Jekyll: v3.5.1. `sudo gem install jekyll`
	
	- Install [NodeJS](https://nodejs.org/) and [Bundler](http://bundler.io/).
	
	- Open terminal. Enter the project's home directory.
	
	- Install dependencies for this project. Using `bundle install`. If there have permisson issues, intuitively try `sudo`.
	
	-  Then run `bundle exec jekyll serve --config _config.yml,_config-dev.yml`
 
	- Open it in your browser: `http://localhost:4000`
	
	- Test your app with `bundle exec htmlproofer ./_site`

3. Github pages.
	- Create a new repo.
	
	- Clone this repo to you local machine.
	
	- Move the contents of the blog to that repo folder.
	
	- Then run: `git add .`, `git commot -m "first commit"`, `git push origin master`. By now, if everything is fine, then typing `Your-Username.github.io` on you browser, you are able to see the blog.

4. Domain name.
5. Disqus configurations.
	

## Settings

You must fill some informations on `_config.yml` to customize your site.

```
name: John Doe
bio: 'A Man who travels the world eating noodles'
picture: 'assets/images/profile.jpg'
...

and lot of other options, like width, projects, pages, read-time, tags, related posts, animations, multiple-authors, etc.
```

## How To?

Check the [FAQ](./FAQ.md) if you have any doubt or problem.

---

[MIT](http://kopplin.mit-license.org/) License © Sérgio Kopplin
