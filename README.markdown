rfsync
------

`rfsync` keeps your files in (r)sync.



USAGE
-----

List backups with `rfsync`:

    $ rfsync
    documents
    pictures
    work


Run a backup with `rfsync <backup>`

    $ rfsync documents


`rfsync` will also pass along any options to rsync, allowing dry runs
and such:

    # check what's going to happen
    $ rfsync -n documents

    # shhh!
    $ rfsync -q documents

    # loudly delete stuff
    $ rfsync -v -d documents



SETUP
-----

Your backup configs are kept in `~/.config/rfsync/`. Files are regular
shell scripts which will be `source`d at run time. These scripts can
contain pretty much anything you like as long as a few environment
variables are set:


* `SRC`

  An array of source directories.

* `DEST`

  A single destination. This can be anything rsync accepts as a
  destination (e.g. local directory, remote server, etc.)

* `EXCLUDE` (optional)

  An array of patterns for rsync to ignore.

* `REQUIRE_DEST` (optional)

  Fail if the destination does not already exist. set to a non-empty
  to string to indicate truthiness. This is not very useful for remote
  destinations.

* `RSYNC_ARGS` (optional)

  An array of arguments to pass onto `rsync`. These are passed before
  any other arguments given on the command line when invoking `rfsync`
  itself.



EXAMPLES
--------

    # ~/.config/rfsync/documents
    SRC=(~/Documents)
    DEST=/mnt/backups/Documents
    REQUIRE_DEST=True

    # ~/.config/rfsync/misc
    SRC=(~/var/log ~/var/mail)
    DEST=user@example.com:backups/misc
    EXCLUDE=(~/var/tmp)

    # ~/.config/rfsync/work
    SRC=~/Work
    DEST=/mnt/backups/Work
    EXCLUDE=(~/Work/secret_project)
