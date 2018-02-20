Heroku buildpack: Kibana - adjusted for using it as in Production UI webpage
================================================================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) that serves up [kibana](https://www.elastic.co/downloads/kibana).

Purpose
-------------
the ADMIN_BUTTONS_VIS_URL variable allows turning off all other tabs of Kibana and only allows access to the Dashboard tab. Also disables saving or modifiying of graphics.   

Compatibility
-------------

Tested against kibana 4.4.0.
works with Elasticsearch 2.4

Usage
-----

    $ cat .buildpacks
    https://github.com/issueapp/heroku-buildpack-kibana

    # for new project
    $ heroku create --buildpack https://github.com/issueapp/heroku-buildpack-kibana

    # for existing project
    $ heroku buildpacks:set https://github.com/issueapp/heroku-buildpack-kibana

    $ heroku config:set ELASTICSEARCH_URL="https://user:pass@elastic.cluster.com:9200"
    $ heroku config:set DOWNLOAD_URL="https://download.elastic.co/kibana/kibana/kibana-4.1.0-linux-x64.tar.gz"
    $ heroku config:set ADMIN_BUTTONS_VIS_URL="navbar\x20button\x20{\n\x20\x20visibility:\x20hidden\x20!important;\n\x20\x20padding:\x205px\x2015px;"
    $ cat Procfile
    web: kibana --port $PORT

    $ git push heroku master

    # verify and profit!
    $ heroku open
