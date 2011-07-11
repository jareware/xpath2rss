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

You should see a usage message.  PHP 5.3+ is recommended, but the script should run with anything 5+.

Usage
-----

The command expects a path to a configuration file as its only argument.  The configuration file is a traditional ini-file that specifies what to fetch, the XPath expressions to use etc.  You can test out a configuration file by running:

    $ xpath2rss --test myconfig.ini

You'll see some useful info.

XPath2RSS essentially maintains a hash-map in the generated RSS-file: the key and the value are queried from the HTML with your XPath expressions.  If a new key is encountered, it's added to the feed.  If the key has already been seen, it won't be added again.

The script is likely most useful when ran from a cron-like facility periodically.

Examples
--------

### A webcomic ###

To get a feed from one popular webcomic (yes, they already have one but this came to mind first), set up an `xkcd.ini` along these lines:

    feedTitle = "xkcd"
    fromURL = "http://xkcd.com/"
    toFile = "/path/to/your/webroot/xkcd.xml"
    keyXPath = "//div[@id='middleContent']//img/@alt"
    valXPath = "//div[@id='middleContent']//img/@src"
    descrTemplate = "<img src='%val%' />"

And run:

    $ xpath2rss --test xkcd.ini

You should see the name of the latest comic as the key and its URL as the value.

### Episodic YouTube-content ###

Some good stuff on YouTube doesn't have its own channel (from which you could get a feed directly).  To gather a feed from the search page, you could do something like:

    feedTitle = "When Cheese Fails"
    fromURL = "http://www.youtube.com/results?search_type=videos&search_query=when+cheese+fails&search_sort=video_date_uploaded"
    toFile = "/path/to/your/webroot/whencheesefails.xml"
    keyXPath = "//div[@id='search-results']//a[ contains(@title, 'Season') and contains(@title, 'Episode') ]/@title"
    valXPath = "//div[@id='search-results']//a[ contains(@title, 'Season') and contains(@title, 'Episode') ]/@href"
    descrTemplate = "<a href='http://www.youtube.com%val%'>View on YouTube</a>"

This works because the search results are ordered newest first, and the XPath expressions will always use the first match if multiple are found.

See also
--------

 1. http://www.w3.org/TR/xpath/ - XPath syntax
