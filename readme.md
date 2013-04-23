# Heroku Binary Buildpack

Use it if you need Heroku to execute a binary.

## Usage

Create Heroku app with this buildpack and clone it:
```bash
$ heroku create APP --buildpack https://github.com/Ph3nx/heroku-binary-buildpack.git
$ heroku git:clone APP
```


Create a bin folder in your app and set the $PATH variable in Heroku:
```bash
$ mkdir APP/bin
$ cd APP
$ heroku config:set PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/app/bin
```


Your App is now ready to use. Put binary files in your the /bin directory. Here is an example of an executable that will run on 64bit linux machine:
```bash
$ echo -e "#\!/usr/bin/env bash\n echo hello world" > ./bin/program
$ echo -e "program: bin/program" > Procfile
$ chmod +x ./bin/program
```


Test the program locally:
```bash
$ ./bin/program
hello world
```


Push the app to Heroku and run our executable:
```bash
$ git add -A; git commit -am 'init'
$ git push heroku master
$ heroku run program
Running `program` attached to terminal... up, run.8663
hello world
```


## Issues

You will need to make sure that a 64bit linux machine can execute the binary.
