---
layout: post
title: Need to install MySQL gem for OSX?
tags:
- mac
- osx
- ruby
- gem
- mysql
- jgp
alias: [/post/54206126,/post/54206126/need-to-install-mysql-gem-for-osx]
---
... but getting errors?

```
matthew@iRudy:~/code/rails211again $ sudo gem install mysql
Password:
Building native extensions.  This could take a while...
ERROR:  Error installing mysql:
ERROR: Failed to build gem native extension.

/System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/ruby extconf.rb install mysql
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lm... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lz... yes
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lsocket... no
checking for mysql_query() in -lmysqlclient... no
checking for main() in -lnsl... no
checking for mysql_query() in -lmysqlclient... no

*** extconf.rb failed ***
...
Gem files will remain installed in /Library/Ruby/Gems/1.8/gems/mysql-2.7 for inspection.

Results logged to /Library/Ruby/Gems/1.8/gems/mysql-2.7/gem_make.out
```

Found the [fix](http://sos.blog-city.com/sudo_gem_install_mysql_on_os_x_with_proper_parameters.htm)

``` ruby
sudo gem install mysql -- --with-mysql-config=/usr/local/mysql/bin/mysql_config
```
