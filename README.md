## Reference

* [Diesel - Get Started](http://diesel.rs/guides/getting-started/)
* [diesel/examples/postgres at master · diesel-rs/diesel · GitHub](https://github.com/diesel-rs/diesel/tree/master/examples/postgres)

## Install DB

```bash
$ brew install postgres
```

```bash
$ initdb --locale=C -E UTF-8 /usr/local/var/postgres
```

```bash
$ pg_ctl -D /usr/local/var/postgres start
```

## Create Database

```bash
$ psql postgres
postgres=# create database foodb owner weli encoding utf8;
CREATE DATABASE
```

## Setup database connection

Edit `.env` file and change the user name used for the postgres connection. 

## Add diesel

```
$ cargo install diesel_cli --no-default-features --features postgres
```

## Run the migration

```bash
$ diesel migration run
Running migration 2020-08-16-065644_create_posts
```

Check the created table in postgres:

```bash
$ psql foodb                                                                                                                                                                                                                    15:51:35
psql (12.4)
Type "help" for help.

foodb=# \dt
                  List of relations
 Schema |            Name            | Type  | Owner 
--------+----------------------------+-------+-------
 public | __diesel_schema_migrations | table | weli
 public | posts                      | table | weli
(2 rows)

foodb=# 
```

## Write post

```bash
$ cargo run --bin write_post                                                                                                                                                                                                    15:29:32
   Compiling diesel_demo v0.1.0 (/Users/weli/works/diesel_demo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.58s
     Running `target/debug/write_post`
What would you like your title to be?
Hello world

Ok! Let's write Hello world (Press CTRL+D when finished)

Hello world, the answer is 42.
^D
Saved draft Hello world with id 1
$
```

## Publish post

```bash
$ cargo run --bin publish_post 1                                                                                                                                                                                               15:41:25
   Compiling diesel_demo v0.1.0 (/Users/weli/works/diesel_demo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.61s
     Running `target/debug/publish_post 1`
Published post Hello world
```

## Show posts
 
```bash
$ cargo run --bin show_posts                                                                                                                                                                                                    15:43:48
   Compiling diesel_demo v0.1.0 (/Users/weli/works/diesel_demo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.43s
     Running `target/debug/show_posts`
Displaying 1 posts
Hello world
-----------

Hello world, the answer is 42.

$                                       
```

## Delete post by title

```bash
$ cargo run --bin delete_post "Hello world"                                                                                                                                                                                     15:44:59
    Finished dev [unoptimized + debuginfo] target(s) in 0.01s
     Running `target/debug/delete_post 'Hello world'`
Deleted 1 posts
```