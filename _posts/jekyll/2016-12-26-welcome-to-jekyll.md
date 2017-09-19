---
layout: post
title: "Jekyll"
comments: true
categories: jekyll
---

## Jekyll
Jekyll is a simple, blog-aware, static site generator. It takes a template directory containing raw text files in various formats, runs it through a converter (like Markdown) and our Liquid renderer, and spits out a complete, ready-to-publish static website suitable for serving with your favorite web server. Jekyll also happens to be the engine behind GitHub Pages, which means you can use Jekyll to host your project’s page, blog, or website from GitHub’s servers for free.

##Installation via RubyInstallerPermalink

[RubyInstaller](https://rubyinstaller.org/) is a self-contained Windows-based installer that includes the Ruby language, an execution environment, important documentation, and more.

1. Download and Install a package manager version from [RubyInstaller Downloads](https://rubyinstaller.org/downloads/).
    
    If problem to download MSYS2, can download manually from [MSYS2](https://sourceforge.net/projects/msys2/files/Base/x86_64/msys2-x86_64-20161025.exe/download) & install it.
2. Install Jekyll and Bundler via a command prompt window: 

```gem install jekyll bundler```
3. Check if Jekyll installed properly: 

```jekyll -v```
4. To start a new project named my_blog, just run:
   
   ```jekyll new my_blog```
   
4. run jekyll project -
```
bundle exec jekyll serve
```
or
```
jekyll serve
```

## Exception
if any problem like 
```
Could not find public_suffix-2.0.4 in any of the sources (Bundler::GemNotFound)
```
for version miss matching just update the gem-
```
bundle update
```