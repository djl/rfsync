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


Use the `-n` or `--dry-run` flag to see what would be synced:

    $ scully -n documents



SETUP
-----

`scully` reads from an INI-style config file called `~/.scully`. Each
section of this file corresponds to a single backup.

Each section can contain the following options:


* `src`

  A comma-separated list of files and directories to be synced.

* `dest`

  Where the sources should be synced to.

* `exclude` (optional)

  A comma-separated list of files to be ignored from `src`.

* `delete` (optional, boolean, default: false)

  Delete extraneous files from destination directories.

* `require_dest` (optional, boolean, default: false)

  Fail if the destination does not already exist.



EXAMPLE
-------

    [documents]
    src = ~/Documents
    dest = /mnt/backups/Documents
    require_dest = True

    [misc]
    src = ~/var/log, ~/var/mail
    dest = user@example.com:backups/misc
    exclude = ~/var/tmp
    delete = true

    [work]
    src = ~/Work
    dest = /mnt/backups/Work
    exclude = ~/Work/secret_project
