notmuch-lore
============
Read [public-inbox] mailinglists via [notmuch].

Being subscribed to high-volume mailinglists can be very damaging to
your mail quota. [public-inbox] solves that problem by offering a Git
front-end to a mailinglist. So instead of trying to download 27k
emails over IMAP and have your provider start to throttle your
requests to a ridiculously low rate (allegedly) after 2k, you can
download Git packs at line rate.

The problem with [public-inbox] is that it is not easy to consume from
regular mail readers. This is where notmuch-lore comes in. It connects
to [public-inbox] repos, downloads messages, and converts them to a
standard Maildir format.


Setup
-----
It is intended to be used as a `pre-new` hook together with
[notmuch]. All you need to setup is an INI file containing a section
per list you want to sync, specifying the URL. Here is an example
config that would track the "netdev" mailinglist from
`lore.kernel.org`:

    [netdev]
    url=https://lore.kernel.org/netdev

This file must be called `sources` and live in the `.lore` directory
in your [notmuch] directory. Typically it will look something like
this:

    ~/mail/.notmuch/
    ├── hooks
    │   └── pre-new -> location-of/notmuch-lore/pre-new
    └── .lore
        └── sources

If you then tell [notmuch] to fetch new mail, e.g. by pressing `G`
from the `*notmuch-hello*` buffer if you are using the emacs mode, you
will sync up your local Maildir to the [public-inbox].

[public-inbox]: https://public-inbox.org/
[notmuch]: https://notmuchmail.org/


