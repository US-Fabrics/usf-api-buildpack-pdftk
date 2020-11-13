# USF API PDFtk Buildpack 

This is a custom buildpack that will install pdftk into /app/bin on Heroku. Currently configured to support heroku-18 which usf-api is on right now.
This will also hard force some default ENV variables like port, PATH, LD_LIBRARY etc...

```
much of this is modeled from a similar project at https://github.com/ardalann/heroku-pdftk-buildpack
```

## How to use

1. Add this buildpack to your app.  Specify this url https://github.com/US-Fabrics/usf-api-buildpack-pdftk

## How to upgrade PDFTK

You'll need to do this if heroku moves to a new version.  USF is currently running on heroku-18.  Update the tarball_url line in scripts/build.sh

`heroku create`

`heroku config:set BUILDPACK_URL=https://github.com/US-Fabrics/usf-api-buildpack-pdftk`

`git push heroku master`

Now you'll have a new Heroku app on the default stack (currently cedar-14) that runs the `scripts/build.sh` script in this buildpack. That script will download the most recent PDFTK source and configure it with default options.

Use `heroku logs -t` to see when compilation is done. It'll start showing dots..

`heroku open`

1. Download the generated pdftk.zip
2. Chmod +x them
3. put them into `bin/$STACK/` into this buildpack. $STACK shall be the name of your stack as given in the Heroku $STACK variable.

`heroku ps:scale web=0` to turn off the dyno.
