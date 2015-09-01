# Deployment #

## Ruby Applications ##

We use [capistrano](http://capistranorb.com/) to deploy our applications to our
development, staging, and production environments.

For applications using Rails, the following capistrano plugins should be
included in the project Capfile.

```
require 'capistrano/setup'
require 'capistrano/deploy'
require 'capistrano/rbenv'
require 'capistrano/bundler'
require 'capistrano/rails/migrations'
```

Here is a reference [config/deploy.rb](https://github.com/ucsdlib/damspas/blob/master/config/deploy.rb)

Note: A secrets.yml should be included for the project in the Stash
private_config repository.



