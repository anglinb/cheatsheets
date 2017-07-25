Postgres
====

Quick note: Wherever you see `YOUR_USERNAME`, you should replace that with your username. In my case, that is `brian`. So if these instructions told me to run `CREATE DATABASE YOUR_USERNAME;` I would run `CREATE DATABASE brian;`.

### Install

**Mac OSX**
    
    brew install postgres
    brew services start postgresql # This will use launchd to start Postgres at login 

_Optional Setup_ 

PSQL is the command line interface the ships with Postgres to allow you to interact with it and run queries. 

    psql postgres  # Open psql and connect to the database named "postgres"

This logs into Postgres w/ the postgres user. By default you won't have an account. I've seen this error like 5 billion times 🙃

    psql: FATAL:  database "brian" does not exist

"*Fix*" this by creating a database with your name b/c postgres will default to logging in with these options: `user`:`YOUR_USERNAME`, `password`:`none`, `database`:`YOUR_USERNAME`. If the database `YOUR_USERNAME` does not exist (which it doesn't by default) the psql w/o arguments will fail.

    psql postgres # Open psql and connect to the database named "postgres"
    CREATE DATABASE YOUR_USERNAME; # Create a database name YOUR_USERNAME (Remember to actually replace YOUR_USERNAME w/ your actual username)

From now on, you can just run 
  
    psql # Yay! No need for typing extra args
   

**Windows**
  
  PRs welcome :D 

### PSQL ([Stolen from @Kartones](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546))

If run with `-E` flag, it will describe the underlaying queries of the `\` commands (cool for learning!).

Most `\d` commands support additional param of `__schema__.name__` and accept wildcards like `*.*`

- `\q`: Quit/Exit
- `\c __database__`: Connect to a database
- `\d __table__`: Show table definition including triggers
- `\dt *.*`: List tables from all schemas (if `*.*` is omitted will only show SEARCH_PATH ones)
- `\l`: List databases
- `\dn`: List schemas
- `\df`: List functions
- `\dv`: List views
- `\df+ __function__` : Show function SQL code. 
- `\x`: Pretty-format query results instead of the not-so-useful ASCII tables

User Related:
- `\du`: List users
- `\du __username__`: List a username if present.
- `create role __test1__`: Create a role with an existing username.
- `create role __test2__ noinherit login password __passsword__;`: Create a role with username and password.
- `set role __test__;`: Change role for current session to `__test__`.
- `grant __test2__ to __test1__;`: Allow `__test1__` to set its role as `__test2__`.

