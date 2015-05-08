+++
date = "2015-02-26T13:29:48-08:00"
menu = "main"
title = "01 - Introduction"
+++

# What is *freedom.js*, and why should I care?
*freedom.js* is a JavaScript framework that facilitates developing
[peer-to-peer (P2P)](https://en.wikipedia.org/wiki/Peer-to-peer)
applications. These sorts of applications have been around for awhile
and can be pretty nifty - they give the developer a low-cost way to
scale up a resilient application, and they give users more control
over their own data. But building them can be challenging, requiring a
sophisticated understanding of networking and security. Doing so in
the browser - the increasingly important yet constantly changing
application platform - is even harder.

This is where *freedom.js* comes in - we provide a framework where
common functionality (social, storage, network transport, etc.) has a
standard interface and a suite of providers that run across typical
JavaScript platforms (currently Chrome, Firefox, and Node.js). Want to
write an app that lets people connect directly to each other in their
browsers, choosing their friends from existing social networks?
*freedom.js* takes care of the details, letting you focus on your
application logic.

How does this work? You'll learn more throughout the tutorial, but the
core of it is that a *freedom.js* app specifies its API and dependencies
via a manifest, and then *freedom.js* uses
[web workers](https://en.wikipedia.org/wiki/Web_worker) to run the
application and related modules. These modules run independently and
so must communicate (message passing via the specified API), but this
isolation and abstraction allows for applications to run across
computers and users - resulting in decentralized peer-to-peer applications.

*freedom.js* is open source
([Apache License 2.0](http://opensource.org/licenses/Apache-2.0))
and you can find our repositories on
[GitHub](https://github.com/freedomjs). We're actively developing and
enhancing the platform, and welcome community contributions. One of
the best ways to get started is to just use *freedom.js* to develop an
application - so think some about what you want to make, and read on!

# What are some apps that have been built using *freedom.js*?
To get an idea of the sorts of things you can do with *freedom.js*, here
are some existing applications:

- __Take Turns, Sally__
([repo](https://github.com/ryscheng/taketurns),
[app](http://taketurns.sally.wtf/)) - a *freedom.js* application that
exposes a simple queue. Everyone in the meeting pops open their
laptop/smartphone and navigates to the URL. Agree on a "room name" and
choose 1 leader in the group. Then queue up to talk!
- __uProxy__ ([repos](https://github.com/uproxy),
[homepage](https://www.uproxy.org/)) - a browser extension that lets
users share alternative more secure routes to the Internet. It's like
a personalized VPN service that you set up for yourself and your
friends. uProxy helps users protect each other from third parties who
may try to watch, block, or redirect users' Internet connections.
- __Dorabella__ (links forthcoming) - an encrypted chat application,
allowing users to generate and exchange keys to secure their further
communication. This is the application that we will build together in
this tutorial - you'll learn about social and cryptography providers,
as well as general *freedom.js* module design and structure.

*freedom.js* also has
[demo apps](http://www.freedomjs.org/dist/freedom/latest/demo/) that
can serve as useful examples while developing (including a chat demo
that is the base of Dorabella).

# Tutorial outline
The tutorial steps through the development of Dorabella, mentioned
above. If you're a new developer then soldiering on in order is
probably a good idea, but if you're already comfortable with the
JavaScript ecosystem then picking and choosing or skipping through may
make sense. The topics of the remaining sections are:

- [Dev Environment Setup](../02devsetup) - the basic commands you need to
  install *freedom.js* and related development tools
- [How *freedom.js* works](../03howfreedomworks) - an explanation of the control
  and messaging flow of a *freedom.js*-powered application
- [Designing Dorabella](../04dorabelladesign) - how to plan the structure and
  API of an app
- [The core of Dorabella](../05dorabellacore) - once it's planned, how to get
  started implementing the boilerplate and beyond
- [Implementing chat](../06dorabellachat) - the main task of Dorabella, and a
  tour of the *freedom.js* social interface
  - [Using crypto in *freedom.js*](../07dorabellacrypto) - an important but
  sensitive part of development, also provided by *freedom.js*
- [Polishing Dorabella](../08dorabellapolish) - testing, automation, and those
  other tweaks that make an app ready to go
- [Deployment and Beyond](../09deploymentandbeyond) - now that the app is
  written, it's time to get it out there
  - [How to help *freedom.js*](../10howtohelpfreedom) - we're an open source`:w
  `
  project and welcome contributions!
