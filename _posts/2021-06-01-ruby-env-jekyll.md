---
layout: post
title: Setting up a Ruby dev environment for Jekyll
description: 
summary: 
---

Download with Brew

```
brew install ruby rbenv
rbenv init
```

Add to .zshrc

```bash
export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"
eval "$(rbenv init - zsh)"
export GEM_HOME="$(ruby -e 'puts Gem.user_dir')"
export PATH="$PATH:$GEM_HOME/bin"
```

```
gem install bundler jekyll
```

```
jekyll new sitename
cd myblog
bundle exec jekyll serve
```

localhost:4000