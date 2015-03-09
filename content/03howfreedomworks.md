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

    src/index.html
    src/main.js
    src/manifest.json
    src/static/style.css

These files are your freedom.js module - they specify layout/browser
logic (`index.html`), freedom.js application logic (`main.js`),
freedom.js API and dependencies/permissions (`manifest.json`), and
styling or other static resources such as graphics (`static/`). In the
above list they all live off of `src/` to reflect that they are the
source code view of your application - they may later be linted,
minified, and copied to e.g. `build/` (to eventually be deployed).

TODO more explanation for how above files interact.

Depending on your choice of tooling, you may also have files like:

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
develop freedom.js modules, but should you find yourself wanting to
dig deeper then here are some places to start:

- [freedom.js wiki](https://github.com/freedomjs/freedom/wiki) - more
documentation and API reference
- [npm docs](https://docs.npmjs.com/) - more on how to both get
packages from npm and deploy your own
- [git](http://git-scm.com/) - there's many tutorials out there, but
[Git from the Bottom Up](http://jwiegley.github.io/git-from-the-bottom-up/)
is a fine place to get started, and [tryGit](http://try.github.io)
is a quick interactive tutorial
- TODO more

It's also valuable to learn about developing traditional (centralized)
web applications. freedom.js requires thinking differently (especially
about data storage and peer communication), but it's useful to
understand both perspectives. There is a fair amount of skill overlap
(understanding templates, network requests, etc.), and for many
"real-world" use cases a hybrid approach of centralized and
decentralized may be best. We will see this in the design of
Dorabella, which pragmatically depends on centralized social networks
as how most users keep track of and communicate with their friends.
