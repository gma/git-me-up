git-me-up
=========

git-me-up was written to automate the creation of a local git repo for a Rails
app that is hosted in Subversion. It should work equally well for non Rails
projects.

In a nutshell, this is what it does:

  - Clones the latest version of the source (by default skipping the history
    for performance reasons) into a new local Git repository.

  - Recreates empty directories (that git chooses to ignore), but that your
    app might need.

  - Converts any svn:ignore Subversion properties into entries in your
    .git/info/exclude file.

  - Checks for Rails plugins installed via svn:externals and clones them into
    their own git repositories (located in a new directory called ./plugins,
    relative to your working directory). Each external plugin is symlinked
    into vendor/plugins. Git is then instructed to ignore them so that it
    doesn't attempt to commit the symlink back into Subversion.

  - Creates a local working branch (called "work" by default; override it by
    setting the BRANCH environement variable).

All this happens in a manner that avoids adding Git metadata (such as
.gitignore files) to your subversion repository.

Install
-------

To install git-me-up into /usr/local/bin, run:

    $ sudo make install

You will need to install git-svn before you can use git-me-up.

Usage
-----

You need to specify two arguments; the Subversion repo that you will be
checking back into, and the path (relative to your current directory) of the
Git repository that you'd like to create.

For example:

    $ git-me-up http://svn.mydomain.com/repo/project/trunk project

By default git-me-up will pull the latest version of your code from
Subversion, ignoring all the history. If you want to override the revision
pulled, set the REVISION environment variable, like this:

    $ REVISION=123:HEAD http://svn.mydomain.com/repo/project/trunk project

See the coverage of the -r option in the git-svn(1) man page for more examples
of how to specify the revision.

Give it a whirl. If you don't like it, delete your local directory. No harm
done...
