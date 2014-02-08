# Heroku Binary Buildpack

Use this buildpack if you want to execute binaries on Heroku. APP is the name of your heroku app. For some commands you need to append "-a APP" or change the directory to the local folder of your app with
```
$ cd /path/to/folder
```

## Usage

Create Heroku app with this buildpack and clone it:
```bash
$ heroku create APP --buildpack https://github.com/ph3nx/heroku-binary-buildpack.git
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
$ echo "program: bin/program" > Procfile
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

You could also add this buildpack to an exesting heroku app:
```bash
$ heroku config:set BUILDPACK_URL=https://github.com/ph3nx/heroku-binary-buildpack.git -a APP
Setting config vars and restarting cmds... done, v3
BUILDPACK_URL: https://github.com/ph3nx/heroku-binary-buildpack.git
```


## Issues

You will need to make sure that a 64bit linux machine can execute the binary.
