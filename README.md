# openbsd-ansible-s3-backup
this is a playbook to set up an automated backup system utilizing AWS S3 as a storage location

## What it does:
* Downloads the dependencies (inotify-tools and awscli)
* Configures an aws profile to connect to (*using already established credentials*)
* Uploads a listener script
    * The listener script runs inotifywait on a directory, when things change it creates an encrypted tarball of the files in the directory
* Uploads an upload script
    * The upload script uploads all encrypted tarballs in a directory and removes them from the local filesystem
* Starts listeners and runs them in the background
* Sets up cron to run at 0300 local time everyday

## Getting Started
Simply put, all you should have to do is set the ansible variables in the `hosts` and the `group_vars/host/vars.yml` files to the values you want, and then run the playbook.

## Notes
* It is currently set up to run `su` as the become method, so if you want to use a different method, you'll have to change that.
* Python 3.6 is used, so make sure that is set up. I have a playbook to set that up as well: [openbsd-ansible-init](https://github.com/desnudopenguino/openbsd-ansible-init).
