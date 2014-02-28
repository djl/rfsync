scully
------

`scully` keeps your files in (r)sync.

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


`scully` will also pass along any options to rsync, allowing dry runs
and such:

    # check what's going to happen
    $ scully -n documents

    # shhh!
    $ scully -q documents

    # loudly delete stuff
    $ scully -v -d documents



SETUP
-----

Your backup configs are kept in `~/.scully/`. Files are regular shell
scripts which will be `source`d at run time. These scripts can contain
pretty much anything you like as long as a few environment variables
are set:


* `SCULLY_SRC`

  An array of source directories.

* `SCULLY_DEST`

  A single destination. This can be anything rsync accepts as a
  destination (e.g. local directory, remote server, etc.)

* `SCULLY_EXCLUDE` (optional)

  An array of patterns for rsync to ignore.

* `SCULLY_REQUIRE_DEST` (optional)

  Fail if the destination does not already exist. set to a non-empty
  to string to indicate truthiness. This is not very useful for remote
  destinations.



EXAMPLES
--------

    # ~/.scully/documents
    SCULLY_SRC=(~/Documents)
    SCULLY_DEST=/mnt/backups/Documents
    SCULLY_REQUIRE_DEST=True

    # ~/.scully/misc
    SCULLY_SRC=(~/var/log ~/var/mail)
    SCULLY_DEST=user@example.com:backups/misc
    SCULLY_EXCLUDE=(~/var/tmp)

    # ~/.scully/work
    SCULLY_SRC=~/Work
    SCULLY_DEST=/mnt/backups/Work
    SCULLY_EXCLUDE=(~/Work/secret_project)
