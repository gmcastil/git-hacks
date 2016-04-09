 Startup with GitHub
=====================

This is a very basic tutorial on how to get up and running with an open source
project that is hosted on GitHub.  It does not cover nearly all of the features
of git but it should get you up.  This is really just a list of steps that I
found myself repeating a lot and had noted in my `~/code/` directory.  I
figured that if I found it useful, others might too.

Configuring SSH
---------------

Before doing anything else, make sure that the appropriate keys are installed
and placed in the right location.

1. Assuming no SSH keys exist, generate new public and private key
   pairs::

     $ ssh-keygen -t rsa -C "your_email@example.com"

   Add the new key to the ssh-agent::

     $ eval "$(ssh-agent -s)"
     $ ssh-add ~/.ssh/id_rsa

   Instructions taken from:

   https://help.github.com/articles/generating-ssh-keys/

2. Copy the public key to the clipboard::

     $ cd ~/.ssh
     $ cat ./id_rsa.pub | pbcopy

3. Add this to the acceptable keys under your GitHub account

4. Now check to make sure that it works::

     $ ssh -T git@github.com

You should see a message telling you that you are authenticated, but
that no shell access is provided (for obvious reasons).

Clone the Forked Copy
---------------------

Fork the upstream repository that you want to work on (e.g., NumPy) into your
GitHub account (you will probably need to do this from the web interface).

1. Now clone a local copy::

  $ git clone git@github.com:USERNAME/<forked repo>.git <local name>

2. Add this as the `origin` repository::

     $ cd <local_name>
     $ git remote add origin git@github.com:USERNAME/<forked_repo>.git

   To the show the `origin` repository as being the forked one::

     $ git remote -v

   It should show that your own copy is being used as the original
   repository.

3. Now add the upstream repository::

     $ git remote add upstream git@github.com:UPSTREAM_USERNAME/<upstream_repo>.git

   List remote repos and you should see something like the following::

     $ git remote -v
     origin	git@github.com:gmcastil/scipy.git (fetch)
     origin	git@github.com:gmcastil/scipy.git (push)
     upstream	git@github.com:scipy/scipy.git (fetch)
     upstream	git@github.com:scipy/scipy.git (push)

Sync a Forked Repo
------------------

1. Fetch upstream branches from the upstream repository.  Commits to
   `master` will be stored in a local branch, `upstream/master`.::

     $ git fetch upstream

2. Check our your fork's local `master` branch::

     $ git checkout master
     Switched to branch 'master'

3. Merge the changes from `upstream/master` into the local `master`
   branch.  This brings your local fork's `master` branch into sync
   with the upstream repository, without losing your local changes.::

     $ git merge upstream/master

   Now, to update your fork on GitHub, push any and all changes to the
   remote::

     $ git push <REMOTENAME> <BRANCHNAME>

   This is usually something like `git push origin master`, where
   `origin` is the forked repo on GitHub and `master` is the local
   master branch, which has been updated from the upstream repository.
     
Links
-----

This looks helpful:

https://help.github.com/categories/collaborating/
