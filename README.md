# MH-Export

Export MH mail files and folders into other mailbox formats, for
example in preparation for uploading them to an IMAP server

The [MH Message Handling
System](https://en.wikipedia.org/wiki/MH_Message_Handling_System)
stores each mailbox message in a separate file. Some other mail-handling tools
instead store entire message folders in a single file, using the
[MMDF](http://www.tin.org/bin/man.cgi?section=5&topic=mmdf) or
[mboxrd](http://www.qmail.org/qmail-manual-html/man5/mbox.html) file
formats.

This Perl script packs the list of MH message files or folders
provided on the command line into a single MMDF or mboxrd file, which
it then sends to standard output. (The MH tool ```packf``` serves a
similar purpose but lacks a number of important features that can lead
to a loss of information.)

## Typical application

If you want to migrate your MH folders onto an IMAP server, first use
this tool to prepare an MMDF mailbox file, which you can then upload
via IMAP using the ```mailutil copy``` tool from the [University of
Washington IMAP distribution](http://www.washington.edu/imap/).

Example:

```
$ mh-export ~/Mail/path/to/mh/folder >~/folder.mmdf && \
> mailutil copy folder.mmdf {imap.hermes.cam.ac.uk/tls/user=crsid}new-folder
```

This will create `new-folder` on the IMAP server and will fill it with
all messages found in `~/Mail/path/to/mh/folder/`. The IMAP folder
`new-folder` must not already exist. (If you want to append messages
to an existing folder, first upload them to a temporary new folder,
then use any IMAP client to move them over to the intended destination
and delete the uploaded and now empty temporary folder.)

## Installation

This repository contains just a single executable script file
`mh-export`. Copy it to wherever you want. There are no dependencies
other than Perl.

I personally have `$HOME/local/bin` in my `$PATH` environment variable
and I install git repositories that contain just one or more script
files, like this one, using
[stow](https://www.gnu.org/software/stow/), like this:

    $ mkdir -p ~/local/bin/stow
    $ cd ~/local/bin/stow
    $ git clone https://www.cl.cam.ac.uk/~mgk25/git/mh-export
    $ stow mh-export

## Documentation

For the complete documentation:

    $ perldoc mh-export

## Author

[Markus Kuhn](https://www.cl.cam.ac.uk/~mgk25/), Computer Laboratory, University of Cambridge
