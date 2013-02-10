---
layout: post
title: a better :delegate method?
tags:
- code
- delegate
- rails
- core
- patch
alias: [/post/54206510,/post/54206510/a-better-delegate-method]
---
So we have;

``` ruby
class Bum
  attr_accessor :pants
  delegate :smelly?, :to => :pants
end
```

We want to ask;

``` ruby
bum.smelly?
```

clearly if the bum has pants, then it's only smelly if the pants are smelly
that's cool,
but what if the bum has no pants?

``` ruby
>> bum.pants
=> nil

>> bum.smelly?
   NoMethodError: You have a nil object when you didn't expect it!
   The error occurred while evaluating nil.smelly?
     from (__DELEGATION__):2:in `__send__'
     from (__DELEGATION__):2:in `smelly?'
     from (irb):7
```

this needs to be fixed,
but how?
by default we'd expect it to be nil,
but perhaps we want to assume that actually they're smelly by default
but what syntax?

```
delegate :smelly, :to => :pants, :default => true
```

perhaps?
