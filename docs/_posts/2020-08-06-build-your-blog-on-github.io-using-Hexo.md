---
layout: post
title: Build your blog on github.io using Hexo
---

## What is Hexo

The [official site](https://hexo.io/) describes Hexo as

> A fast, simple & powerful blog framework.

It compiles the Markdown text to the beautiful HTML page. Those pages can not only be hosted on your own server, but can also be hosted on the github.io.

## Install the Hexo

1. Install the [nodejs](https://nodejs.org/en/) and [git](https://git-scm.com/) if you do not have them installed.

2. Open the terminal/Powershell, enter `npm install hexo-cli -g` to install Hexo.

3. Enter `hexo --version`. If you see something like `hexo-cli: 4.1.0`, then it is installed. The version might differ.

## Create a Hexo blog

### Initialize the project

`cd` the folder where you want the project to be. `hexo init your_blog_name` to initialize the Hexo project. Replace the `your_blog_name` with your actual project name. The command will clone the site prototype from the Github and populate the dependency.

When you see the command finished with `INFO  Start blogging with Hexo!`, then you are good to go.

### Serve the blog locally

```bash
cd your_blog_name
hexo server
```

If you get the error like `FATAL Port 4000 has been used. Try other port instead.` Add `-p 4001` or `-p 4002` to `hexo server` until you find an available port. If you want the server to listen on the specified IP, add `-i <ip address>` to the command.

Now open the browser and go to [http://localhost:4000](http://localhost:4000), change the address and the port if you specified them before, then you will see your blog!

## Start to write

### Create a new post

While the server is running, open another terminal on the project folder, then `hexo new "The post name"` to create a new post. The post file is in the `<your_project_name>/source/_posts` folder.

### Edit the new post

Open the newly created `The-post-name.md` file, you can start to write your post. The file will contain some texts between `---` at the start. It is called the **front matter**. It adds metadata to your post, like title, date, tag, category, etc. for the Hexo to generate archives, categories, and more for the posts. You can learn more about the front matter [here](https://hexo.io/docs/front-matter.html).

After the front matter, the text will be parsed as Markdown. You can use the [Github Markdown Cheatsheet](https://github.com/adam-p/Markdown-here/wiki/Markdown-Cheatsheet) if you are not familiar with the Markdown syntax. There are also some good Markdown editors, like [Typora](https://typora.io/) for Windows, macOS and Linux, which is also the editor for this site, or [MacDown](https://macdown.uranusjr.com/) for macOS, [Remarkable](https://remarkableapp.github.io/linux.html) for Linux. You could also use Vim, Emacs, VSCode or plain text editor if you like.

## Configure the blog

### The configuration file

The configuration file is in the project root folder, and named `_config.yml`. It is written with YAML syntax. For more about the YAML, you can start a quick tutorial [here](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html) or check the [official document here](https://yaml.org/spec/1.2/spec.html).

### Edit the configuration

The configurations are quite straightforward. If you have questions on certain options just check the [official document](https://hexo.io/docs/configuration). Some important options are

```yaml
title: 'The site title'
author: 'Your Name'
# The language code, change it if your site is not in English.
# The full list is https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes
language: en
# Change your timezone, the timezone format is in Moment.js format,
# you can check a list of timezone on https://momentjs.com/timezone/
timezone: ''

# URL
url: http://yoursite.com
```

## Generate and deploy the blog

Finally you can publish your blog online. `npm install --save hexo-deployer-git` or `yarn add hexo-deployer-git` if you use yarn to add the deployer. 

Open the configuration file `_config.yml`. Scroll down to the end of the file. Replace the deploy section with

```yaml
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  # example, https://github.com/hexojs/hexojs.github.io
  branch: gh-pages
```

`<project>` should be your domain. It is usually `<username>.github.io`.

Then run `hexo clean && hexo deploy`. When the deployment finished, go to [https://username.github.io](https://<username>.github.io) to see your blog!

If you choose to use CI to deploy the blog, please see [the document](https://hexo.io/docs/github-pages).

## Going further

You can [install the theme](https://hexo.io/docs/themes) for the blog, [add plugins](https://hexo.io/docs/plugins) or customize it by yourself, or compile your posts by the date, the categories and the tags. Just have fun and enjoy your blog.

## Copyright

This post is written by chryoung. You can copy/paste if you cite the source.

## References

1. [Official document](https://hexo.io/docs/)
2. [How to use Hexo and deploy to GitHub Pages](https://gist.github.com/btfak/18938572f5df000ebe06fbd1872e4e39)
