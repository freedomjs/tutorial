+++
date = "2015-02-26T13:25:07-08:00"
menu = "main"
title = "05 - The core of Dorabella"
+++

In this section we will flesh out the core of the main *freedom.js* module for
Dorabella, providing the API functionality needed for the overall application.
We will leave the specifics of interacting with the modules we depend on for
later sections, and focus on giving an overall picture of how the module works.

# Starting the module
TODO

# Implementing the API
TODO

# Making the implementation usable
To invoke methods in the module, they must be made visible to *freedom.js*. This
is similar to how node.js modules export their functionality, but in
*freedom.js* we will invoke a method such as `providePromises`. This will tell
*freedom.js* that the object we constructed above satisfies the API specified in
the manifest (`securechat.json`)


TODO
