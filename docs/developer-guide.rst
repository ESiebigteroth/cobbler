Developer Guide
---------------


Patch process
+++++++++++++

You'd like to contribute features or fixes to Cobbler? Great! We'd love to have them.

It is highly recommended that you have a github.com account if you would like to contribute code. Create an account, log in, and then go to github.com/cobbler/cobbler to "fork" the project.

Create a new branch named after the feature you are working on. Do the work on your local machine, please make sure your work passes Cobbler's coding standards by using `make qa`. Only then push to your personal Github branch (e.g. github.com/yourname/cobbler).

Then use the "submit pull request" feature of Github to request that the official repo pull in your changes. Be sure to include a full description of what your change does in the comments, including what you have tested (and other things that you may have not been able to test well and need help with).

If the patch needs more work, we'll let you know in the comments.

Do not mix work on different features in different pull requests/branches if at all possible as this makes it difficult to take only some of the work at one time, and to quickly slurp in some changes why others get hammered out.

Once we merge in your pull request, you can remove the branch from your repo if you like. The AUTHORS file is created automatically when we release.


Setup
+++++

The preferred development platform is the latest version of Fedora and/or CentOS. You'll also have to disable SELinux to get Cobbler up and running.

For CentOS you will need the EPEL repository: ``http://download.fedoraproject.org/pub/epel/7/x86_64/repoview/epel-release.html``

Install development dependencies:

.. code-block:: none

    # yum install git make openssl python-sphinx python36-coverage python36-devel python36-distro python36-future python36-pyflakes python36-pycodestyle python36-setuptools rpm-build

Install runtime dependencies:

.. code-block:: none

    # yum install httpd mod_wsgi python36-PyYAML python36-netaddr python36-simplejso m
    # pip3 install Cheetah3

Initially, to run Cobbler without using packages:

.. code-block:: none

    # git clone https://github.com/<your username>/cobbler.git
    # cd cobbler
    # make install

For each successive run, do not run make install again. To avoid blowing away your configuration, run:

.. code-block:: none

    # make webtest

This will install Cobbler and restart apache/cobblerd, but move your configuration files and settings aside and restore them, rather than blindly overwriting them.

You can now run Cobbler commands and access the web interface.


Branches
++++++++

Cobbler has a development branch called "master" (where the action is), and branches for all releases that are in maintaince mode. All work on new features should be done against the master branch. If you want to address bugs then please target the latest release branch, the maintainers will then cherry-pick those changes into the master branch.

.. code-block:: none

    # git branch -r
    # git checkout <branch>
    # git checkout -b <new branch name>


Standards
+++++++++

We're not overly picky, but please follow the python PEP8 standards we want to adhere to (see Makefile).

* Always use under_scores, not camelCase.
* Always four (4) spaces, not tabs.
* Avoid one line if statements.
* Validate your code by using ``make qa``.
* Keep things simple, keep in mind that this is a tool for sysadmins and not python developers.
* Use modules that are easily available (eg. EPEL) but preferrably in the base OS, otherwise they have to be packaged with the app, which usually runs afoul of distribution packaging guidelines.
* At least for now we have to support Python 2.7 for Cobbler and ython 2.6 for Koan.

You're also welcome to hang out in #cobbler and #cobbler-devel on irc.freenode.net, as there are folks around to answer questions, etc.


Contributing to the website
+++++++++++++++++++++++++++

The github-based git repository for the https://cobbler.github.io website itself is at https://github.com/cobbler/cobbler.github.io.

If you want to contribute changes to the website, you will need jekyll (http://jekyllrb.com).

You will probably want to:

* edit the files in _dynamic
* run the generate_dynamic.sh script
* add both the .md and resulting .html files in your git commit


Mailing List
++++++++++++

We have a development mailing list at https://fedorahosted.org/mailman/listinfo/cobbler-devel
Discuss development related questions, roadmap, and other things there, rather than on the general user list.

It is a very good idea to mention your pull request (copy/paste, etc) to the development mailing list for discussion.


Debugging
+++++++++

If you need to debug a remote process, epdb provides some very nice capabilities beyond the standard python debugger, just insert a "import epdb; epdb.serve()" in your command line, and from the console:

.. code-block:: none

    # python -c "import epdb; epdb.connect"

