Custom buildpack: Factor
=======================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks).

Usage
-----

Example usage:

    $ heroku buildpacks:add --index 2 "https://github.com/vishvananda/heroku-buildpack-factor"

    $ git push heroku main
    ...
    -----> Factor Buildpack app detected
    -----> Attempting to rewrite Procfile
           Added factor to web command:
           web: ./factor ./start.sh

The buildpack will detect if your app has a `Procfile` in the root and rewrite
the web process to use [factor](https://github.com/twelve-factor/factor) to run
your your app.

In order for factor to work you will need to enable dyno metadata:

    $ heroku labs:enable runtime-dyno-metadata -a <app name>

And you will also need to create a secret:

    $ heroku config:set -a <app name> FACTOR_SECRET=$(openssl rand -base64 32)
