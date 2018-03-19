#### I decided to make a post for my future self or anyone else who might want to recreate a Heroku server using a postgres db on a local environment. Here's how I did it.

#### I originally set up my application to use a sqlite3 DB, but since I wanted to deploy to Heroku which doesn't support sqlite. Be sure to note that what I'm doing might reflect swapping from sqlite3.
#BACKROUND (LIGHT READING)
#### https://www.postgresql.org/

#SETUP
### I'm on a mac and never done this with windows. For the Mac link I only went down to the `Start PostgreSQL` section, for what we're doing I didn't need to log in.
### for mac users :http://exponential.io/blog/2015/02/21/install-postgresql-on-mac-os-x-via-brew/
### for window users :https://www.postgresql.org/download/windows/

#ALMOST THERE!
### add `gem 'pg'` to gemfile if not already.
### add `gem rails_12factor` to both as well
### make changes to your database.yml file
### in terminal $`$bundle install`
### if you haven't started your DB server yet start it by opening a new tab in terminal and running $`postgres -D /usr/local/var/postgres`
### create, migrate, seed: in terminal $`RAILS_ENV=development rake db:create db:migrate db:seed` (depending on if you want this db `production` or `development` you would change those part out)
### in terminal and copy output $`rake secret`
### run $`export SECRET_KEY_BASE=<paste secret key>` NO SPACES secret...key> and don't need the `<` and `>`
### run $`rake assets:precompile`
### run $`RAILS_ENV=development rails s` for this if your RAILS_ENV is already development you can just run `rails s` (depending on if you want this db `production` or `development` you would change those part out)
### Remember to clobber your assets (rake assets:clobber)-removing old precompiled assets -  and re-precompile (rake assets:precompile)- precompiles assests -  if you make changes. to drop a db run `dropdb <name>` sometimes `rake db:drop` works

#Finished
### At this point your DB should be up and running and you should be able to run your server and have it functioning. qu
