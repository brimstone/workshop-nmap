nmap Options
============

nmap has a ton, TON, of options. Read more about them with `man nmap` or [in
the book](https://nmap.org/book/man-briefoptions.html)

My favorite options are `-vv -oG scan.out -A`

Verbosity
---------

You might have noticed the scan took a bit before returning results. Start nmap
with: `-v` or `-vv` to make nmap more verbose for the duration of the scan.

If a scan is already in progress and taking longer than you thought, press `v`
or `V` to increase or decrease verbosity without restarting.

OS Detection
------------

nmap can attempt to detection the operating system with `-O`


Logging to a file
------------------

Results of the scan can be logged to a file with one of the following:
- `-oN` normal, just like what's on the screen
- `-oX` XML format
- `-oG` Grepable format

Combo options
-------------

The `-A` option enables all of the following:
- `-O` OS detection
- `-sV` Version detection
- `-sC` script scanning
- `--traceroute` traceroute

Ports
-----

By default, nmap scans 1,000 common ports out of the possible 65,535 total. You
can change this with:

- `-F` Fast scan, only 100 ports than the default
- `-p 22,80,135` Scan for only 22, 80, and 135.

Even more
---------

The links in the resources on the front page mention more of nmap's features,
even going into a deep dive on some of them.

Try to find all of the webservers on the network.

_Hint: They will have port 80 open._
