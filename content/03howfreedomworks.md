+++
date = "2015-02-26T13:27:01-08:00"
menu = "main"
title = "03 - How freedom.js works"
+++

*Note* - this section isn't integral to building a simple app,
 but it is valuable to get a slightly deeper understanding of the
 stack you are building on. You can
 [safely skip to the next section](../04dorabelladesign) if you wish,
 and potentially revisit here for reference as needed.

# Understanding the boilerplate
Regardless of how you chose to [do your dev setup](../02devsetup),
you should now have a file hierarchy that looks something like this:

    src/freedom-module.js
    src/freedom-module.json
    src/index.html
    src/page.js
    src/static/freedomjs-icon.png
    src/static/style.css

These files are your *freedom.js* module - they specify layout/browser
logic (`index.html` and `page.js`), *freedom.js* application logic
(`freedom-module.js`), *freedom.js* API and dependencies/permissions
(`freedom-module.json`), and styling or other static resources such as graphics
(`static/`). In the above list they all live off of `src/` to reflect that they
are the source code view of your application - they will later be copied to
`build/` (and possibly linted and minified in the process).

`index.html` and `page.js` work much like simple static web pages you may be
familiar with - the browser renders the page according to the HTML and runs
JavaScript logic directly in the browser (i.e. it can interact with the DOM -
the page itself). You can think of this as the "front end" of your application,
though it is important to understand that the "back end" (the freedom module)
also runs on the client. The main difference is that the freedom module runs in
a web worker that cannot interact directly with the DOM, and instead uses
message passing defined by its API to interact with and update the webpage.

Web workers are a standard intended to enable the concurrent execution of
multiple JavaScript threads - a prototypical use would be to [calculate
something computationally expensive (e.g. large prime numbers)]
(http://dev.w3.org/html5/workers/#a-background-number-crunching-worker)
while not interfering with the user interface. *freedom.js* uses these workers as
module containers, which combined with an enforced API leads to a clearer
picture of the behavior of the overall application.

The demo application you have from your setup is "Counter", a simple example of
how freedom modules run and pass messages. You should definitely be able to run
the demo locally (either with the `runserver.sh` script or with `grunt demo` if
you chose to use npm), but you can also
[view Counter at freedomjs.org](http://www.freedomjs.org/dist/freedom/latest/demo/counter/)
for convenience.

The functionality of the application is simple - click the button to increment
the displayed count. The key insight is that the displayed count is part of the
webpage and is updated through the DOM, but the incrementing itself occurs in
the *freedom.js* module. Following is the program flow - see if you can find the
lines of code corresponding to each step (answers are linked but see if you can
first find the spots without peeking).

1. The browser loads the page and *freedom.js* is loaded with a given manifest
(*[answer](https://github.com/freedomjs/freedom-starter/blob/master/src/page.js#L21-27)*)
2. *freedom.js* running in the browser creates the initial freedom module object
(*[answer](https://github.com/freedomjs/freedom-starter/blob/master/src/page.js#L12)*)
3. The freedom module itself is instantiated from the given starting value
(*[answer](https://github.com/freedomjs/freedom-starter/blob/master/src/freedom-module.js#L9-12)*)
4. The browser listens for clicks on the incrementing button
(*[answer](https://github.com/freedomjs/freedom-starter/blob/master/src/page.js#L14)*)
5. The browser sends a message to the freedom module on receiving incrementing clicks
(*[answer](https://github.com/freedomjs/freedom-starter/blob/master/src/page.js#L15)*)
6. The freedom module receives the message and returns the incremented value
(*[answer](https://github.com/freedomjs/freedom-starter/blob/master/src/freedom-module.js#L14-18)*)
7. The browser receives the value back and updates the page
(*[answer](https://github.com/freedomjs/freedom-starter/blob/master/src/page.js#L16)*)

The above flow may seem painstakingly detailed for such a simple example, but
it is wise to make sure you understand every step as they will be larger and
more obfuscated in more complex applications. Overall, while all the code is
running in the browser, you need to be able to envision the divide between the
code that interacts with the DOM (in this case `page.js`) and the code that
runs in a web worker (in this case `freedom-module.js`). The former is
responsible for both updating the visible page and handling user interaction
with it, while the latter is responsible for running whatever *freedom.js*
application logic you create, storing state, and communicating that state wtih
the code running directly in the browser. In this specific case, `page.js`
knows about the button clicks and is responsible for updating the displayed
count, while `freedom-module.js` knows the actual count value and increments
and returns it when requested.

The above addresses the starter code that is directly part of a *freedom.js*
module. Depending on your choice of tooling, you may also have files like:

    Gruntfile.js
    node_modules/...
    package.json
    .gitignore

These are best understood by looking up their respective
documentation, as described below.

# Other resources
Any piece of computer technology is inevitably built on a deep stack
eventually going down to [sand and physics](http://xkcd.com/1349/) -
this tutorial focuses on giving you enough knowledge and context to
develop *freedom.js* modules, but should you find yourself wanting to
dig deeper then here are some places to start:

- [*freedom.js* wiki](https://github.com/freedomjs/freedom/wiki) - more
documentation and API reference
- [npm docs](https://docs.npmjs.com/) - more on how to both get
packages from npm and deploy your own
- [git](http://git-scm.com/) - there's many tutorials out there, but
[Git from the Bottom Up](http://jwiegley.github.io/git-from-the-bottom-up/)
is a fine place to get started, and [tryGit](http://try.github.io)
is a quick interactive tutorial
- TODO more

It's also valuable to learn about developing traditional (centralized)
web applications. *freedom.js* requires thinking differently (especially
about data storage and peer communication), but it's useful to
understand both perspectives. There is a fair amount of skill overlap
(understanding templates, network requests, etc.), and for many
"real-world" use cases a hybrid approach of centralized and
decentralized may be best. We will see this in the design of
Dorabella, which pragmatically depends on centralized social networks
as how most users keep track of and communicate with their friends.
