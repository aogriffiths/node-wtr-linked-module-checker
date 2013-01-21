```
                                 .("""")                                      (j)
                               (_(_ __(_ )                                 (n o d e)
 _ _ _       _                   / / /                       (n)              (s)
 ))`)`) ___  )L __ __           / / /           n            \|/              \|/
((,(,' ((_( (( (('(|             n             \|/            |                |
```
Part of the [Node Water](https://github.com/aogriffiths/node-wtr) collection. 

* __linked-module-checker__ - Help node.js module development flow more freely.
    * On [github.com](https://github.com/aogriffiths/node-wtr-linked-module-checker)
    * On [npmjs.org](https://npmjs.org/package/linked-module-checker)

Useful if you are growing your node project, with or without any other node water.

So What Does it Do?!
--------------------

It checks the modules in your node_moudles directory and reports on their status, 
specifically if they are linked (e.g. `npm link`ed) or installed (e.g. `npm install`ed)
and if they are staged to be committed by git (e.g. `git add`ed).
 
The problem lmc really solves is when you are:
1. npm linking your modules during development; and
2. git committing your node_moudles directory; and
3. bored of needing to switch to and from linked vs installed modules each time you git commit. 

Is This Really A Problem I Need To Worry About?
-----------------------------------------------
Maybe not, but you've read this far so read on...

Splitting your node.js project into modules is a good thing. npm linking modules during 
development can really save you time. git committing your node_modules is also a good thing
as Mikeal Rogers [neatly summaries](http://www.futurealoof.com/posts/nodemodules-in-git.html).

However if you accidentally git commit your node modules while they are npm linked your 
source code won't be in a great state. The symlinks created by npm link are unlikely to work
on any machine other than your own so when you git clone/pull/push your project somewhere else
it is unlikely to run without some manual npm tinkering first. Even worse, unless you have done
some diligent publishing of your module elsewhere it may not be possible to get hold of the right
version to make your project run at all. 

lmc helps you avoid these problems.

Installation
------------

Official releases can be obtained from:
* __github.com__ - the [tags section](https://github.com/aogriffiths/node-wtr-linked-module-checker/tags) 
                   provides links to zip or tar.gz packages. 
* __npm__        - use `npm install -g linked-module-checker`

The lastest developed code may node have not have been released, but can always be found
from:
* __github.com__ - the [project homepage](https://github.com/aogriffiths/node-wtr-linked-module-checker)
                   provides links to all the source code, branches and issue tracking.
                   
Help
----
See the output of lmc --help

Integration with Git
--------------------

Add this to you git pre-commit:

    `lmc -e`

Credits
=======

* Isaac Z. Schlueter - https://github.com/isaacs/npm

