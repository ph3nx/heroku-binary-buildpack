# heroku-null-buildpack

Use it if you need Heroku to execute a binary.

## Usage

Create a directory for our Heroku app:

```bash
$ mkdir -p myapp/bin
$ cd myapp
```

Here is an example of an executable that will run on 64bit linux machine:

```bash
$ echo -e "#\!/usr/bin/env bash\n echo hello world" > ./bin/program
$ echo -e "program: bin/program" > Procfile
$ chmod +x ./bin/program
$ ./bin/program
hello world
```

Push the app to Heroku and run our executable:

```bash
$ git init; git add .; git commit -am 'init'
$ heroku create --buildpack https://github.com/Ph3nx/heroku-null-buildpack.git
$ git push heroku master
$ heroku run program
Running `program` attached to terminal... up, run.8663
hello world
```

## Issues

You will need to make sure that a 64bit linux machine can execute the binary.
