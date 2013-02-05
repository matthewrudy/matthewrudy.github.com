---
layout: post
title: Stop adding methods to Symbol just to make your DSL look pretty!
tags:
- ruby
- api
- symbol
- sql
---
I remember the first time I saw [Datamapper](http://datamapper.org).

I liked saying `:something.gt something_else`.

It was pretty.

But after a while I realised it wasn't necessary.

So why are we still building APIs that involve extending Symbol?

``` ruby
# is this really more ugly than
User.where(:age => {:gt => 20})
# this?
User.where(:age.gt => 20)

# is this really more ugly than
User.sort([:age, :desc])
# this?
User.sort(:age.desc)

# Do I really want Symbol to have all of these methods?
Symbol.unnecessary_instance_methods == [
  :gt,
  :lt,
  :gte,
  :lte,
  :ne,
  :in,
  :nin,
  :mod,
  :all,
  :exists,
  :asc,
  :desc
]
```

I saw [this](http://railstips.org/blog/archives/2010/06/16/mongomapper-08-goodies-galore) on an extension called [Plucky](http://github.com/jnunemaker/plucky) for [MongoMapper](http://github.com/jnunemaker/mongomapper).
