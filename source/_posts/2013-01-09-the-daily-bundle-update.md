---
layout: post
title: The daily `bundle update`
tags:
alias: [/post/40050292827, /post/40050292827/the-daily-bundle-update]
---

A typical process for me is like this.

I start off with

* a dependency on Rails 3.1.10
* a dependency on any version of koala

So my Gemfile says exactly this

``` ruby Gemfile
gem "rails", "3.1.10"
gem "koala"
```

Every day I do a `bundle update`.
Sometimes there are new versions of gems, sometimes there aren't.

One day there is a new version of koala released `koala (1.6.0)`

When I do my daily bundle update everything breaks. It turns out that `koala (1.6.0)` relies upon `faraday (0.8)`.

For some reason this breaks my app.

So I realise I have a new dependency, and I add it to my Gemfile.

``` ruby
gem "rails", "3.1.10"
gem "faraday", "0.7" # 0.8 breaks for some reason
```

Dealing with these problems in small doses, on a daily basis, makes it easier to deal with.
