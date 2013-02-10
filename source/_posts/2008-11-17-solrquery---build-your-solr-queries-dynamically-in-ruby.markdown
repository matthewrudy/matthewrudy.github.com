---
layout: post
title: SolrQuery - build your solr queries dynamically in Ruby
tags:
- ruby
- solr
- fulltext
- search
- github
- plugin
alias: [/post/60175045,/post/60175045/solrquery-build-your-solr-queries-dynamically-in-ruby]
---
I’ve been using ActsAsSolr for about 6 months.

And at work I developed some code to make SOLR queries work a bit like
the conditions in ActiveRecord.

Check out my library at Github.
[http://github.com/matthewrudy/solr_query][]

``` ruby
SolrQuery.build(:keyword => "Feather duster"
#
# "feather duster"

SolrQuery.build(
  :keyword => "clean",
  :organisation => [organisation1, organisation2]
)
# "clean AND organisation:(275 OR 6534)"
```

Wicked!

Check out the readme for more examples.

  [http://github.com/matthewrudy/solr_query]: http://github.com/matthewrudy/solr_query