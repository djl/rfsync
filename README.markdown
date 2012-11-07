scully
------

`scully` keeps your files in sync.

Think of her as the more conservative, skeptical partner of
[mulder](https://github.com/djl/mulder).



USAGE
-----

List backups with `scully`:

    $ scully
    documents
    pictures
    work


Run a backup with `scully <backup>`

    $ scully documents



SETUP
-----

`scully` reads from an INI-style config file called `~/.scully`. Each
section of this file corresponds to a single backup.

Each section can contain the following options:


* `source`

  A comma-separated list of files and directories to be synced.

* `destination`

  Where the sources should be synced to.

* `exclude` (optional)

  A comma-separated list of files to be ignored from `source`.

* `delete` (boolean, default: false)

  Delete extraneous files from destination directories.

* `require_destination` (boolean, default: false)

  Fail if the destination does not already exist.



EXAMPLE
-------

    [documents]
    source = ~/Documents
    destination = /mnt/backups/Documents
    require_destination = True

    [misc]
    source = ~/var/log, ~/var/mail
    destination = user@example.com:backups/misc
    exclude = ~/var/tmp
    delete = true

    [work]
    source = ~/Work
    destination = /mnt/backups/Work
    exclude = ~/Work/secret_project
