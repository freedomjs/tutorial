+++
date = "2015-02-26T13:21:22-08:00"
menu = "main"
title = "09 - Deployment and Beyond"
+++

Deploying a *freedom.js* application is as easy as serving the static resources
that compose it. As an example, we will use
[GitHub Pages](https://pages.github.com/) as a convenient static host that can
be deployed right along side your application repository.

To use GitHub pages we just need to:

- Create a `dist` directory containing what we want to deploy
- Set up a `gh-pages` branch as a subtree of the master repository
- (Optional) provide a CNAME file so we can use our own domain
- (Optional but good idea) automate the deploy process with e.g. a Grunt task

You can
[read GitHub document](https://help.github.com/categories/github-pages-basics/)
for more details, and in general these principles should apply to other static
hosts.

We will use
[grunt-build-control](https://www.npmjs.com/package/grunt-build-control) to
facilitate the process. `grunt-build-control` makes it simple to set up and
manage branches. The Grunt task needs to specify a remote target as well as
related options (the local directory to commit, the message to add, etc.).
[See the Dorabella task](https://github.com/soycode/dorabella/blob/master/Gruntfile.js#L76-90)
as an example.
