# Heroku Binary Buildpack
Use this buildpack if you want to execute binaries on Heroku. APP is the name of your Heroku app. For some commands you need to append `--app APP` or change the directory to the application's folder.

## Usage
Create Heroku app with this buildpack and clone it:
```bash
$ heroku create APP --buildpack https://github.com/ph3nx/heroku-binary-buildpack.git
$ heroku git:clone --app APP
$ cd APP
```

Set the $PATH variable in Heroku:
```bash
$ heroku config:set PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/app/bin
```

Your Heroku app is now ready to use. Next create a bin directory for your binaries and a simple executable. 
```bash
$ mkdir bin
$ echo -e "#\!/usr/bin/env bash\n echo hello world" > ./bin/program
$ echo "program: bin/program" > Procfile
$ chmod +x ./bin/program
```

Note, to work on Heroku, executables must run on 64bit Linux. You can test the executable locally like this:
```bash
$ ./bin/program
hello world
```

Push the app to Heroku and run our executable:
```bash
$ git add -all; git commit -m 'init'
$ git push heroku master
$ heroku run program
Running `program` attached to terminal... up, run.8663
hello world
```

You could also add this buildpack to an existing heroku app:
```bash
$ heroku config:set BUILDPACK_URL=https://github.com/ph3nx/heroku-binary-buildpack.git -a APP
Setting config vars and restarting cmds... done, v3
BUILDPACK_URL: https://github.com/ph3nx/heroku-binary-buildpack.git
```

## Issues
You will need to make sure that a 64bit Linux machine can execute the binary.
