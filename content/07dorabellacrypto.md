+++
date = "2015-02-26T13:23:10-08:00"
menu = "main"
title = "07 - Using crypto in freedom.js"
+++

In this section we will use the PGP API along with a trustworthy cryptography
provider to employ signing/encryption and verifying/decryption in a *freedom.js*
application.

*An aside* - you may be thinking "isn't
 [JavaScript cryptography considered harmful](http://matasano.com/articles/javascript-cryptography/)?"
 For some applications and threat models it surely is, but
 [it can also be useful](http://vnhacker.blogspot.co.uk/2014/06/why-javascript-crypto-is-useful.html),
 and our purpose and usage of it here is appropriate for a few key reasons:

- **Our modules run in web workers** - this means they can only
  communicate with the DOM via message passing, and reduces the
  "malleable runtime" problem.
- **We're using modern audited crypto code** - specifically the
  provider we'll be using depends on Google's
  [End-to-End](https://github.com/google/end-to-end), which implements
  Elliptic Curve Cryptography and is also
  [being used by Yahoo Mail](http://yahoo.tumblr.com/post/113708033335/user-focused-security-end-to-end-encryption).
  The PGP API also can be used with other providers, if you prefer.
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
`freedom-pgp-e2e` is a *freedom.js* module that takes care of setting up and
properly invoking the crypto operations implemented by End-to-End.
[It is available on npm](https://www.npmjs.com/package/freedom-pgp-e2e), and
can be added to your project by running:

    npm install --save-dev freedom freedom-pgp-e2e

This installs the package to the `node_modules/` path, along with your other
dependencies. You can then add rules to your Gruntfile to automatically copy the
needed files.
[The `path` package can find the files](https://github.com/soycode/dorabella/blob/master/Gruntfile.js#L5-6)
, and
[simple copy rules can copy them](https://github.com/soycode/dorabella/blob/master/Gruntfile.js#L34-41).

In particular, you need the contents of the `dist/` path within the package -
this includes both the End-to-End library (`end-to-end.compiled.js`), the
*freedom.js* PGP API (`pgpapi.json`), and the actual `freedom-pgp-e2e`
implementation (`e2e.js`). The API is worth reading to understand its usage -
the `"_comment"` fields are optional and don't change functionality but do serve
to document the purpose of methods.

To actually use the PGP API, the *Dorabella* API must
[specify its dependence on it](https://github.com/soycode/dorabella/blob/master/src/securechat.json#L17-20)
, referring to the path it is copied to in the Gruntfile, and then
[create a PGP object](https://github.com/soycode/dorabella/blob/master/src/securechat.js#L27)
from the `freedom` object within its own module code. The resulting object will
satisfy the PGP API, allowing us to get started securing our chat application.

# Setting up the crypto client
The PGP API has a setup command that takes two arguments - a passphrase and a
user ID. The passphrase is used to encrypt the local storage of the keyring,
while the user ID is used to identify the keyring. Classically these are how
a user would protect their keyring and associate it with an email - the user ID
format is `name <email>`.

The *Dorabella* use case is slightly different than email - users connect
automatically through a social API. We can grab the user name from this, and
to complete the user ID we choose to provide a default filler email address.
[The email address](https://github.com/soycode/dorabella/blob/master/src/securechat.js#L53)
just serves to indicate that the software is dependent on `freedom.js`, while
not inconveniencing or exposing the user unnecessarily.

Looking at the setup line, you may also notice that we provide a blank
passphrase (the first argument) - this is a conscious choice and accepting a
particular threat model for *Dorabella* - namely, we assume that the local
machine is trusted and secure. Encrypting the local keyring is obviously worthy
for more broad PGP use cases, as well as situations where you expect to travel
or otherwise potentially expose your keyring to risk. With *Dorabella*, the
keyring is generated specifically for the application and the API provides no
method for exporting the private key - this limits the risk of not encrypting
it, and not asking the user for a passphrase increases the convenience of the
application.

This security-convenience tradeoff is an inevitable part of the design of any
security-sensitive application, and you may well personally prefer a different
choice. A worthy extension of *Dorabella* would be to optionally accept a
passphrase, allowing more security-conscious users to better address their
threat models. For now though, we will set up with the blank passphrase and
focus on how to properly use the API after the setup is complete.

# Exchanging keys
TODO - `exportKey` gets the public key, and currently users automatically
exchange on connection. This means that messages are at least encrypted, but
no out-of-band trust is established in the key.

# Using the PGP API to exchange secure messages
The workhorse methods of the PGP API are `signEncrypt` and `verifyDecrypt` -
these operations do what they say on the tin. Specifically, `signEncrypt` can
sign and/or encrypt a message, and `verifyDecrypt` can verify and/or decrypt.
For *Dorabella* we will be both authenticating (signing/verifying) and securely
encoding (encrypting/decrypting) the messages.

TODO finish, also address armoring/dearmoring
