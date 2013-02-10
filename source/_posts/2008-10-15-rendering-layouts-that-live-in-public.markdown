---
layout: post
title: Rendering layouts that live in /public?
tags:
- code
- ruby
- public
- actionview
- layouts
- templates
alias: [/post/54730156,/post/54730156/rendering-layouts-that-live-in-public]
---
At work we have the following concept.

1. a "site" has a subset of our content
2. a "site" has a url - eg. "oursite.com/stickers" or "stickersNOTvicars.com"
3. a "site" can have its own customised layout, or fall back to the default one

How does this work in code?

1. site.articles (pretty simple)
2. a whole load of "route filters" that match the incoming host
3. the code I’m writing about

So, historically we did

``` ruby
class ApplicationController
  layout :determine_layout
  def determine_layout
    if File.exists?("#{Rails.root}/public/sites/#{@site.id}/application.rhtml")
      "../../public/sites/#{@site.id}/application"
    else
      "site_default"
    end
  end
end
```

This was a hack, and it breaks with Rails 2.1.1, so after a day or so playing with the internals of ActionView I discovered this;

``` ruby
append_view_path("#{Rails.root}/public/sites")
```

And it works!

We just need to set;

```
"#{@site.id}/application"
```

as our layout, and we're away.

Site-specific layouts that live in /public!
