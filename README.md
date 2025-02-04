# mlmmj-archivist

A shell script for creating web archives for mlmmj mailing lists. Mlmmj-archivist generates the web archives for the public mailing lists of GFOSS (ΕΕΛ/ΛΑΚ), available at [https://lists.ellak.gr/](https://lists.ellak.gr/).

## Features

- Supports flat and hierarchical mailing list directory structures; eg. both `/var/spool/mlmmj/listname` and `/var/spool/mlmmj/domain.tld/listname` structures are supported.
- Theming support.
- Localization support.
- Also creates introduction pages for the domain and each mailing list.

## Requirements & Compatibility

- [MHonArc](http://mhonarc.org).
- [rsync](http://rsync.samba.org/).
- Basic UNIX utilities: awk, cat, date, grep, install, sed and, of course, sh.

Tested on Debian Wheezy. Currently it requires GNU date so it is not very portable. Should fix this in a future update.

The current Makefile requires GNU make. In future versions it should work with BSD make too.

##OpenBSD installation##


installation :
dependency : we need few packages to run this script 
1. MHonArc.
2. rsync.
3. coreutils

Basic UNIX utilities: awk, cat, date, grep, install, sed and, of course, sh. ( check up )

git clone https://github.com/eellak/mlmmj-archivist.git

cd mlmmj-archivist

sed -i -e "s:date --date:gdate --date:g" mlmmj-archivist.sh

** what it does
to run this on OpenBSD GNU date needed, as we have installed coreutils 
package already it will replace date in the script with gdate.

make install
After completing the installation you should copy the configuration files mlmmj-archivist.conf.sample to mlmmj-archivist.conf, 
and mhonarc.mrc.sample to mhonarc.mrc, and tweak to your preference, prior to running the script

both of the files can be found in /etc/mlmmj-archivist. ( well after installation )

we need to create archivist dir in each mailing list dir

corntab 
*/1      *       *       *       *       /usr/local/bin/mlmmj-archivist

add the above line in crontab to archive the list.

also the PATH one top should look like this
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin

## Installation

Running

<pre><code>make install</code></pre>

should install the script in `/usr/local/bin`, the configuration samples in `/etc/mlmmj-archivist` and the bundled templates in `/usr/local/share/mlmmj-archivist/templates`.

All paths can be adjusted by setting the environment variables:

- `SYSCONFDIR`: for the configuration directory.
- `PREFIX`: for replacing `/usr/local` with something else.
- `BINDIR`: the installation path for the executable script.
- `SHAREDIR`: the shared directory; currently contains the templates directory.
- `DESTDIR`: the root directory to work on. Useful for packaging.

After completing the installation you should copy the configuration files `mlmmj-archivist.conf.sample` to `mlmmj-archivist.conf`, and `mhonarc.mrc.sample` to `mhonarc.mrc`, and tweak to your preference, prior to running the script for first time.

## Usage

`mlmmj-archivist` is designed to run from cron in predefined intervals. Since it creates archives incrementally it can be used with frequent intervals in busy hosts with many mailing list messages.

An example crontab entry for running `mlmmj-archivist` hourly:

<pre><code>5 * * * *  /usr/local/bin/mlmmj-archivist</code></pre>

## TODO

- Add parallel archive creation capability, for SMP systems.
- Switch the localization system to something less hackish; gettext is a good candidate.

## License

This project is licensed under the [ISC license](http://opensource.org/licenses/ISC).
