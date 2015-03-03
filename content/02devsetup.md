+++
date = "2015-02-26T13:28:59-08:00"
menu = "main"
title = "02 - Dev Environment Setup"
+++

# Quick Start
Already comfortable with modern JavaScript development? Then you can
easily get started by using [Yeoman](http://yeoman.io):

    npm install -g yo  # if you don't have yo already
    npm install -g generator-freedom
    mkdir my-freedom-app
    cd my-freedom-app
    yo freedom

Or if you prefer pulling in boilerplate with git:

    TODO

If you're set, skip ahead to
[how freedom.js works](../03howfreedomworks). Need a bit more
explanation on the above? Read on!

# Details
Strictly speaking, all you need to develop with freedom.js is the
[library itself](http://www.freedomjs.org/dist/freedom/latest/freedom.js),
a browser, and a web server (for example,
[SimpleHTTPServer](https://docs.python.org/2/library/simplehttpserver.html)
for Python 2.x). You are welcome to take this minimalist approach,
though you may want to at least
[clone the starter git repository](http://TODO) for boilerplate.

An arguably more convenient setup is to embrace the modern JavaScript
ecosystem. There are many tools and it can be overwhelming at first,
but you really just need to familiarize yourself with a few of them to
get started:

- [npm](https://www.npmjs.com/) - a package manager (installed from
  [nodejs.org](http://nodejs.org/)), lets you fetch freedom.js and
  related modules/dependencies/tooling
- [grunt](http://gruntjs.com/) - a task runner, facilitates linting,
building, testing, and deploying projects
- ... (TODO testing, maybe alternatives like gulp, etc.)

freedom.js is agnostic about the tools you use, but our provided
generators and scripts generally assume use of npm, grunt, TODO (tests
etc.). Getting started means
[installing node and npm](https://docs.npmjs.com/getting-started/installing-node),
then running a variety of `npm install` commands. The common tools
you'll use across projects should be installed globally (`-g`), e.g.:

    npm install -g grunt-cli

Projects themselves can have their own `package.json` file that
specifies dependencies, which are installed locally by simply running
`npm install` in that directory. Once you've set up your project this
way (and have a [Gruntfile](http://gruntjs.com/sample-gruntfile) - an
initial one is provided by our generator) you can run `grunt -h` to
see the available Grunt tasks. They are run with `grunt taskname`, or
just `grunt` for the default task. You can also dive into
`Gruntfile.js` and edit or add your own tasks.

Once you have your setup to your liking, continue on and learn more
about freedom.js itself!
