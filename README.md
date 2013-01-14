node-wtr-dev-workflow-example
=============================

A dev workflow example that might help your node.js project grow.

This example show a way to keep a main project and supporting modules nicely separated
but work on them at the same time and avoid the overhead of copy files arround all the 
time.

Skip the introduction if you want to get straight to it. You can always come back to 
the introduction later!

Introduction
============

Background
----------

Breaking your project into modules has lots of advantages, it helps keep the project 
organised, allows you to split out common functions and to share them with other projects 
or the world via repositories like github.com and npmjs.org.

But there are overheads...

* How does you main project include your module? By copying the files? By using a package 
  manager link npm? Using git sub-modules?
* If you change your module code, how quickly are those changes reflected in your main 
  project? Do you need to do recopying, republishing, pushing, pulling or anything else?
* You want to develop quickly, if one small change to the module takes minutes and you make
  many in a day this gets slow...
* You also want you main project to be self contained. Anyone cloning it should be able
  run it out of the box.
* You might be tempted to, or accidently, work on your module source from within the source 
  tree of you main project and then need to copy back the changes. This can result this can
  result in a whole manor of problems of it's own...

I'll stop with the list. If you've ever been there you know what it's like (and that 
might be why you've read this far!).

Following the approach in the How it Works section you will be able to source control 
both your module and main project independently but develop them together, not worry about 
editing the wrong files and generaly make life easier.

Assumptions
-----------

You are running node.js, npm and git (but I'm sure a similar approach could work with other 
lanaguages, package managers and source control).


Some Set Up
-----------

If you want to play with the approach using an example you can easily make one
yourself or clone mine from github. Follow these steps either way.

1.  Create two repositories on github or clone mine `node-wtr-dev-workflow-example` and 
    `node-wtr-dev-workflow-example-module`

    The first one is the main project, the second is a module that your main 
    project is dependent on.

2.  Make a top level directory on your machine to hold both your main project and your 
    module. e.g. `~/mydevproject/`

3.  Clone both repositories into this top level directory:

    ```bash
    git clone git@github.com:aogriffiths/node-wtr-dev-workflow-example.git
    git clone git@github.com:aogriffiths/node-wtr-dev-workflow-example-module.git
    ```
   
    Your should now have directories something like this:

    ```bash 
    ~/mydevproject/node-wtr-dev-workflow-example/
    ~/mydevproject/node-wtr-dev-workflow-example-module/
    ```

4.  Write some code (e.g. index.js, README.md, package.json etc)

    The module should export something and the main project should require it 
    (otherwise why bother!). If you clone my examples they already do that.

5.  Make like easier 

    ```bash
    sudo chown -R $USER /usr/local/lib/node_modules/
    ```

    This will mean you don't need to run subsequent npm commands as sudo, which 
    is easier and arguably more secure than having /usr/local/lib/node_modules/ 
    belong to root.

How it Works
============

Link
----

Link to the module from the main project with:

```bash
cd ~/mydevproject/node-wtr-dev-workflow-example
npm link ../node-wtr-dev-workflow-example-module/
```
    
see more at https://npmjs.org/doc/link.html.

   
Run your main project with

    node index.js

And everything should work:

* Your main project should be able to use the method you exported from your module.
* Edits to you module via both '~/mydevproject/node-wtr-dev-workflow-example-module/'
and '~/mydevproject/node-wtr-dev-workflow-example/node_modules/node-wtr-dev-workflow-example-module/'
are editing the same files (so no laborious requirement to edit you module in one place and copy
the edits to the other).
* You can work on the code in your module and your main project simultaneously until they both work
* You can git commit your module any time you want
* There is a gotcha with committing your main project. See below.


Install
-------

Once your module is working well within your main project you should install it. See 
http://www.mikealrogers.com/posts/nodemodules-in-git.html

The way to install the working version of your module is similar to the way you linked it during 
development.

    cd ~/mydevproject/node-wtr-dev-workflow-example
    npm install ../node-wtr-dev-workflow-example-module/

Now you can git commit your main project and anyone taking a copy will be able to
run it, as you intended, without needing to find the latest version of the working module, which you
may or may not have published to the npm repository or github.

