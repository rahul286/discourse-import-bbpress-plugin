## move to discourse dir

```
cd ~/Sites/discourse
```

## Start rails app

```
bundle exec rails s
```

## Run importer

```
bundle exec rake import:bbpress
```


## Dump Schema

```
bundle exec rake db:schema:dump
```

## Copy files from docker container to host filesystem

Run `docker ps` to find value of container id (example: `9ca5055dfedd`)

```
docker cp 9ca5055dfedd:/var/www/discourse/lib/tasks/import_bbpress.rake ~
docker cp 9ca5055dfedd:/var/www/discourse/config/import_bbpress.yml ~
```

### Discourse production app starts with

```
cd /var/www/discourse && sudo -E -u discourse bundle install --deployment --verbose --without test --without development
```

### Pass production ENV to rails

```
RAILS_ENV=production
```

## Dump Rails DB Schema

```
RAILS_ENV=development bundle exec rake db:schema:dump
cat db/schema.rb
```

For visual graphs

```
brew install graphviz
echo "gem 'rails-erd'" >> Gemfile
bundle install
bundle exec erd
bundle exec erd --inheritance --direct --attributes=foreign_keys,content
```


## Get Rails Console

```
RAILS_ENV=development bundle exec rails c
u = User.last
u.admin = true
u.save
```


### Discourse Development on MAC

TOFIX: UTF8 template encoding mismatch

```
CREATE DATABASE discourse_development WITH OWNER rahul286 ENCODING 'UTF8' TEMPLATE template0;
CREATE DATABASE discourse_test WITH OWNER rahul286 ENCODING 'UTF8' TEMPLATE template0;

psql -d discourse_development -U rahul286 -h localhost

CREATE EXTENSION pg_trgm;
CREATE EXTENSION hstore;

psql -d discourse_test -U rahul286 -h localhost

CREATE EXTENSION pg_trgm;
CREATE EXTENSION hstore;
```


## mysql debugging

SELECT id, post_title, post_parent, post_type FROM rtc_wp_posts WHERE post_type = 'forum';
SELECT id, post_title, post_parent, post_type FROM rtc_wp_posts WHERE post_type = 'topic';
SELECT id, post_title, post_parent, post_type FROM rtc_wp_posts WHERE post_type = 'reply';
