+++
date = "2015-02-26T13:26:05-08:00"
menu = "main"
title = "04 - Designing Dorabella"
+++

# General architecture
To make any application it is wise to first consider how its overall
functionality is best broken up into separate logical components. A chat
application must perform at minimum:

- Maintenance and reporting of client status (i.e. if you are online)
- Reporting of peer status (i.e. if your friends are online)
- Sending/receiving messages with peers
- Displaying messages sent/received, client/peer online status, etc.

On top of that, we want our particular chat application to sign and encrypt
outgoing messages and verify and decrypt incoming ones. And since we're using
freedom.js, we want to do all of this in as decentralized a manner as possible,
while still building a pragmatic and usable application.

Unfortunately the Internet has not settled on a decentralized social network,
and so the natural way for most users to know if their friends are online and
exchange messages with them is through proprietary services. This will not be
changed in one fell swoop, and so instead our goal will be to write an
application that can at least be used with *any* social network service, so
users can at least switch more freely. And the encryption will also occur
entirely on the client side, reducing the social network to a relatively
uninformed message passing channel.

As we learned in [the previous section](../03howfreedomworks), freedom.js works
by executing concurrent JavaScript threads in web workers that communicate via
message passing. Each web worker is a freedom.js module that should have a
distinct purpose, and there is also typically at least some JavaScript executed
directly in the browser (so it can interact with the user and the DOM). Let us
consider separating our chat application into three modules (not counting the
direct-in-browser code):

- A module to handle interaction with the social network service
- A module to handle encryption/decryption
- A module to handle local client usage and state (essentially to connect the
JavaScript running directly in the browser with the other two modules)

Of these three, we only need to actually write the last one - freedom.js
provides a
[social API](https://github.com/freedomjs/freedom/blob/master/interface/social.json)
as well as some standard providers for us to get started, and we will be using
[freedom-pgp-e2e](https://github.com/freedomjs/freedom-pgp-e2e) to provide
a PGP-like interface for encryption.

So our overall plan for the structure of Dorabella (from "front" to "back") is:

- **User interface** - HTML, static resources (CSS, images)
- **"Outer" JavaScript** - runs directly in browser and not a web worker,
responsible for starting freedom.js, interacting with the main module, and
updating the DOM with new information (as well as general UI/UX niceties)
- **Main freedom.js module** - core of Dorabella, receives messages from
"outer" JavaScript, uses social and crypto modules, and returns results
- **Social API** - built-in freedom.js interface for finding and communicating
with friends via a variety of social media services
- **PGP API** - freedom.js module that provides PGP-style crypto functionality

TODO diagram?

# Component details and API

Now that we have a general idea of the code we want to write, we should plan in
more detail the structure of the main module we'll write. In particular this
means deciding on an API for communicating with outer (DOM-interacting)
JavaScript, and ensuring that this API facilitates all needed uses of the other
(social and crypto) modules.

<table>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Value</th>
    <th>Functionality</th>
  </tr>
  <tr>
    <td>TODO</td>
    <td>TODO</td>
    <td>TODO</td>
    <td>TODO</td>
  </tr>
</table>