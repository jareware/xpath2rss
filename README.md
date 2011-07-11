XPath2RSS
=========

A simple web scraper for querying HTML documents with XPath and turning the results into an RSS feed.

What's it for
-------------

It's for keeping up with the updates to those annoying sites that don't provide an RSS feed themselves.  There's some example cases below.

Installing
----------

On a Debian-like system get the dependencies with:

    $ apt-get install php5-cli php5-curl

Then get yourself a copy of xpath2rss.php (might be handy to drop it in your `PATH` somewhere, like under `/usr/bin`).  Feel free to rename it to `xpath2rss` while you're at it if you don't like the extension (the interpreter is specified in the file).

To see that it's a-OK, try running:

    $ xpath2rss

You should see a usage message.

Usage
-----

The command expects a path to a configuration file as its only argument.  The configuration file is a traditional ini-file that specifies what to fetch, the XPath expressions to use etc.  You can test out a configuration file by running:

    $ xpath2rss --test myconfig.ini

You'll see some useful info.

Examples
--------

TODO

See also
--------

 1. XPath syntax
 1. TODO
