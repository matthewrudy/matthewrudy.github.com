---
layout: post
title: Configuring foreman for Production and Development
tags:
alias: [/post/40470402045, /post/40470402045/configuring-foreman-for-production-and-development ]
---

I follow the convention;

* `Procfile` defines *all* processes
* `.foreman` sets specific foreman variables

Development:

* `.env` sets environment variables for each developer
* `.env.example` sets defaults for development
* `foreman start` starts all processes

Production:

* `heroku config` sets environment variables
* `heroku ps:scale` turns on or off whichever processes are needed for production

Here's an example from a project.

``` ruby Procfile
web: bundle exec unicorn_rails -p $PORT -c ./config/unicorn.rb
worker: bundle exec rake jobs:work
search: bundle exec rake sunspot:solr:run
```

``` ruby .env.example
# default S3 bucket
S3_KEY=keykeykeykeykeykey
S3_SECRET=secretsecretsecret
S3_BUCKET=myapp-development
```

``` ruby .env
# developer's private S3 bucket
S3_KEY=mememememememememe
S3_SECRET=mysecretmysecret
S3_BUCKET=myapp-development
```

``` ruby .foreman
# development port is 3000
port: 3000
```
