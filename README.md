Custom buildpack: Factor
=======================

This is a [Cloud Native Buildpack](https://buildpacks.io).

Usage
-----

Example usage:

    $ git clone https://github.com/jabrown85/heroku-buildpack-factor <clone path>

    $ pack build -B heroku/builder:24 -b <clone path>
    ...
    ===> BUILDING
    [builder] -----> Installing Factor
    [builder] -----> Configuring Factor
    [builder] -----> Processing Procfile
    [builder] Launch process configured with Factor wrapper
    [builder] -----> Factor buildpack installation complete

The buildpack will detect if your app has a `Procfile` in the root and rewrite
the web process to use [factor](https://github.com/twelve-factor/factor) to run
your your app.

In order for factor to work you will need to enable dyno metadata:

    $ heroku labs:enable runtime-dyno-metadata -a <app name>

And you will also need to create a secret:

    $ heroku config:set -a <app name> FACTOR_SECRET=$(openssl rand -base64 32)
