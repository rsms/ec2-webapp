# Workflow

Here we outline three different workflows -- how to hack on and deploy your app.

## Workflow 1: Hack locally, git pull to deploy

This is the recommended workflow as it is robust and every change you make is backed up (in your git repository) and can be reverted at any time.

- Work in your own, local clone of the repository.
- No need to log in to or modify files on the server
- Use the `update` script to deploy changes (update the server)

When developing locally you don't need to have Nginx installed, but simply start your Node.js http server which will handle static files. Very convenient:

    bin/myapp-httpd.mv

And your site is accessible at localhost:3000


### Examples of using the update script

The update script usage: `update [restart|noop [<refspec>]]`

Make some changes and push them live, but don't restart services:

    cd src/myapp
    git commit ...
    ssh -i ~/.ssh/myapp.pem ubuntu@myapp.com:/var/myapp/update
    # some status output here

Make some changes and push them live, also restarting services (Node.js server):

    cd src/myapp
    git commit ...
    ssh -i ~/.ssh/myapp.pem ubuntu@myapp.com:/var/myapp/update restart

Revert to an older version on the server:

    ssh -i ~/.ssh/myapp.pem ubuntu@myapp.com:/var/myapp/update restart v0.1.2

> Note: `v0.1.2` in this example is a tag but can be replaced by any git refspec, like a commit hash or branch name.

You can simplify the "update" call by creating an alias in your `~/.bash_rc` (or other shell startup file):

    alias myapp-update='ssh -i ~/.ssh/myapp.pem ubuntu@myapp.com:/var/myapp/update'

Then, the above example could instead be executed as:

    myapp-update restart v0.1.2


## Workflow 2: Live hack with git

- Hack directly on the server in the `/var/myapp` git repository
- Only recommended if you are alone (i.e. no one else is editing)

To get going with this you need to setup the `/var/myapp` git repository for pushing upstream.

1. Add your SSH key to `/var/www/.ssh/id_rsa` (the one which you are using to access your git repository)
2. Change the repository URI for `/var/myapp` to your read-write URI (i.e. your git@github... URI) with `git remote set-url origin git@github...`

Now, hack away as the `www-data` user and `git push origin` when you feel like it.

Example:

    cd /var/myapp
    # hack hack hack
    sudo invoke-rc.d myapp-httpd restart
    # check if it works
    sudo -uH www-data git push origin

> **Important:** If you add your *private ssh key* to `/var/www/.ssh/id_rsa`, make sure that no web server is running (however, if you have performed the steps in INSTALL.md it's safe to run Nginx). Otherwise you will be exposing your private key. An alternate solution for the reckless mind is to create a dedicated user account.

## Workflow 3: Live hack

- Hack directly on the server in `/var/myapp`
- No git involved and thus no backup or ability to revert from a b0rked server

Simply make a copy of this repo into `/var/myapp` on your server and follow the guide in `INSTALL.md` with exception of checking out your repo.

Example:

    cd /var/myapp
    # hack hack hack
    sudo invoke-rc.d myapp-httpd restart
    # it probably works, let's have a beer and relax
