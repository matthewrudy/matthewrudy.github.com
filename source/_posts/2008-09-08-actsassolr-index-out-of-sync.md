---
layout: post
title: ! 'ActsAsSolr index out of sync?  '
tags:
- ruby
- solr
- acts_as_solr
- fulltext
- search
- jgp
---

Faced with a shocking

``` ruby
>> Phrase.find_by_solr ‘book’
RuntimeError: Out of sync!

The id 296452 is in the Solr index but
missing in the database!
```

Fix it

``` ruby
>> Phrase.solr_delete(“Phrase:296452”)
>> Phrase.solr_commit()
```

BOOM!!!
