+++
date = "2015-02-26T13:23:10-08:00"
menu = "main"
title = "07 - Using crypto in freedom.js"
+++

In this section we will use the PGP api along with a trustworthy cryptography
provider to employ signing/encryption and verifying/decryption in a *freedom.js*
application.

*An aside* - you may be thinking "isn't
 [JavaScript cryptography considered harmful](http://matasano.com/articles/javascript-cryptography/)?"
 For some applications and threat models it surely is, but we believe
 our purpose and usage of it here is appropriate for a few key
 reasons:

- **Our modules run in web workers** - this means they can only
  communicate with the DOM via message passing, and reduces the
  "malleable runtime" problem.
- **We're using modern audited crypto code** - specifically the
  provider we'll be using depends on Google's
  [End-to-End](https://github.com/google/end-to-end), which implements
  Elliptic Curve Cryptography and is also
  [being used by Yahoo Mail](http://yahoo.tumblr.com/post/113708033335/user-focused-security-end-to-end-encryption).
  The PGP api also can be used with other providers, if you prefer.
- **We generate the keypair locally and don't let you export the
  private key** - we
  [generate keys with secure parameters](https://github.com/freedomjs/freedom-pgp-e2e/issues/25)
  and want to ensure those keys stay safe.

Of course, the important remaining issue is that, if you use a
*freedom.js* application by simply visiting a webpage, you are still
trusting that server (and your connection to it) to deliver the true
application on every page load. This can be mitigated by packaging the
application (e.g. as a browser extension or mobile application),
requiring the user to instead trust their application delivery
platform (which pulls new application versions less frequently and is
more likely to have cryptographic signatures and a review process).

Our goal is to provide developers a tool that will allow them to write
applications that are at least *more* private and *more* secure than
many existing models. However, if your adversary is a global passive
attacker or similar powerful entity, then you would be well-advised to
treat any and all online tools and services with skepticism and do
what you can to take your security into your own hands. It is up to
you and your threat model to decide whether or not "some" security is
better than "no" security.

In other words:

- __Do use crypto with *freedom.js* if__ -  you want a bit more privacy
  and control over your data than you get with most existing web
  applications.
- __Don't use crypto with *freedom.js* if__ - you're planning a coup,
  defending yourself from an Advanced Persistent Threat, or want to stop the Men
  in Black from reading your thoughts.

# Getting and loading the freedom-pgp-e2e module

# Setting up the crypto client and handling keys

# Using the crypto API to exchange secure messages
