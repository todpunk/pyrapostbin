# tnl-cookiecutter-first
A simple postbin for self-hosting reliable long-term postbins

This should give you everything you need to access a database with a JSON API you can login against and get a token for.  The user will be `siteadmin` with password `ChangeMe!` which you should definitely change of course.

## Set things up 

Create the database using your favorite method using the following commands as a basis for what you're doing.  If you just run these as a db superuser these will work from the commandline assuming you're in the pyrapostbin root.

```
createdb pyrapostbin
createdb pyrapostbintest
createuser dbuser
psql -d pyrapostbin -c "alter user dbuser with encrypted password 'dbpass'"
psql -d pyrapostbin -c "grant all privileges on database pyrapostbin to user 'dbuser'"
psql -d pyrapostbin -c "grant all privileges on database pyrapostbintest to user 'dbuser'"
psql -d pyrapostbin -a -f pyrapostbin-appsrv/db/schema.sql
psql -d pyrapostbintest -a -f pyrapostbin-appsrv/db/schema.sql
psql -d pyrapostbin -c "insert into users (username, email, password, salt) values ('siteadmin', 'fake@example.com', '', '')"
```

In the appsrv directory, if you haven't already got pyramid and the other bits, do a `pip -r requirements.txt` and then `pserve --reload development.ini` which will get the API server running on 6543 or http://localhost:6543/app/ should get that running.

Frontend dev will be different of course. You should then go into the static directory and do an `npm install` and `npm build`, and if you want to run the react server thing, `npm start` and you can start cracking on whatever!

Yay!