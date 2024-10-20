# lrzsz: free x/y/zmodem implementation

> This is Uwe Ohse's lrzsz with fixes for current compilers (the last official version dates from Decemver 199). The minimal required amount of changes were introduced in order to fix errors when building the tools.
>
> The original code can be found at https://www.ohse.de/uwe/software/lrzsz.html and the original HTML is reproduced below.
>
> #### Tested on
>
> * MacOS with Xcode 15
> * Raspberry Pi with Raspbian 8.3.0
>
> with `make fastcheck`.

* * *

_lrzsz_ is a unix communication package providing the [XMODEM, YMODEM](ftp://ftp.std.com/obi/Standards/FileTransfer/YMODEM8.DOC.1.Z) [ZMODEM](http://www.easysw.com/~mike/serial/zmodem.html) file transfer protocols. lrzsz is a heavily rehacked version of the last public domain release of [Omen Technologies](http://www.omen.com/) _rzsz_ package, and is now [free software](http://www.gnu.ai.mit.edu/philosophy/free-sw.html) and released under the [GNU General Public Licence](http://www.gnu.ai.mit.edu/copyleft/gpl.html).

* * *

### Features of lrzsz

*   very portable, automagically configured with GNU _autoconf_.
*   crash recovery.
*   up to 8KB block sizes (ZMODEM8K).
*   internationalized (using GNU _gettext_). German translation of the programs output exists.
*   far more secure than the original sources.
*   high performance. say \`make vcheck-z' and have a look at the BPS rate - i recently saw _1.4 MB per second_ transfering a large file through pipes (on a I586/133 system. Beat that!).
*   good blocksize calculation (tries to compute an optimal blocksize based on the number of errors occured).
*   It's [free software](http://www.gnu.org/philosophy/free-sw.html).

* * *

### Downloading lrzsz

The lastest release is [lrzsz-0.12.20.tar.gz](https://www.ohse.de/uwe/releases/lrzsz-0.12.20.tar.gz) (_(about 270KB)_).

* * *

### Recent changes

*   Version 0.12.20 - December 1998, Uwe Ohse  
    *   works on BeOS and stone-aged SCO (sco-3.2v4.2)
    *   pubdir-"feature" works again.
    *   "make rpm" creates a rpm file.
    *   "optimal blklen calculation" was too aggressive, it now does nothing if the user demands fixed blklens.
    *   various smaller and medium bug fixes.
    *   a more or less important security bug is fixed (stupid use of /tmp in a piece of code which is rarely used).
    *   lrz uses umask to make files unreadable which receiving them.
    *   "sh systype | mail uwe-generic-counter@ohse.de" sends a success report with a description of the system type.
    *   \--enable-syslog is now default
*   Version 0.12.19 - January 1998, Uwe Ohse  
    (sorry, i forgot to announce that version here. -- uwe, 9.5.1998)
    *   0.12.18 was broken, lsz crashed if receiver found an CRC error.
    *   lrz options "--rename" and "--escape" didn't work.
    *   lrz didn't implement senders "overwrite-or-skip" option.
    *   added dejagnu testsuite. Maybe you need a dejagnu snapshot to use it.
*   Version 0.12.18 - November 1997 **keep off - this version has a major bug**
    *   syslog output now includes user name.
    *   new script lrzszbug, to be used for bugreports (untested)
    *   lots of compiler warnings (egcs -Wparanoia \[many -W\]) removed.
    *   new options --tcp-server and --tcp-client ADDRESS:PORT for both programs. (this is not too much code bloat, and somewhat useful for me - but i suspect nobody else will need it. Oh well)
    *   updated to gettext-0.10.32
    *   updated to automake-1.2
*   Version 0.12.17 - August 1997
    *   internal cleanup.
    *   portability enhancements by (Philippe De Muyter <phdm@info.ulb.ac.be>)
    *   lsz has a new option "--tcp" (no shortopt implemented). lsz transmits one file over normal stdin/stdout (a control file), then opens a tcp connection to transmit all other files.  
        That _might_ be useful if your telnetd is really stupid.This version was \_not\_ put on the ftp/http servers.
*   Version 0.12.16 - March 1997
    *   major performance improvement (less CPU time needed - don't expect faster transfers over slow lines). _make vcheck_ now show about 50% more throughput.
    *   updated to gettext-0.12.27 and automake-1.1l (automake-1.1l bug: AC\_SUBST in AM\_PATH\_PROG\_WITH\_TEST leads to a "$1=@$1@" line in Makefile.in. I hacked around it in /usr/share/aclocal/gettext.m4).
*   Version 0.12.15 - February 1997
    *   lrzsz now compiles even with pre-ANSI-compilers (tested with the HPUX 9.00 bundled compiler - what a bad program. Shame on HP).
    *   lrz supports a new option --o-sync, which forces it to open the output file in synchronous write mode. Don't use it unless you are using interrupts if update writes to the disk.
*   Version 0.12.14 - January 1997
    *   lrzsz now compiles cleaner on SCO, HPUX.
    *   improved error reporting (i think there are still possibilities for further improvements, if anybody case spare time :-)).
*   Version 0.12.13 - January 1997
    *   no user visible changes. just a maintainance release.
    *   updated to gettext-0.12.26.
*   Version 0.12.12 - January 1997
    *   lrx and lrb (aka lsz --x/ymodem) now default to 128 byte block length (to fix interoperatability problems with some Xmodems \[USR courier flash upload\]).
    *   lrz didn't recognize every short option.
    *   minor performance tweaks.
    *   replace mktime() if needed.
    *   updated to autoconf 2.12.
*   Version 0.12.11 - October 1996
    *   lsz/lrz recognize "rshell" as another name for the restricted shell.
    *   lrz/lsz recognize a new option _\--stop-at HH:MM_ (stop transmission at HH:MM), and _\--stop-at +N_ (stop in N seconds).
    *   lrz/lsz recognize a new option _\--delay-startup N_: wait _N_ seconds before doing anything.
    *   doesn't hang anymore on BSD machines after getting a timeout (BSD restarts system calls after an interrupt - this made timeout code useless).
    *   SIGINT handling turned on unter linux too (i still don't know why it was turned off under linux (and only there)).
    *   _sz -_ now prints better transfer statistics after if reading from a pipe.
*   Version 0.12.10 - September 1996
    *   lsz resends init string if it doesn't receive rz's init.
    *   improved "make check". By Philippe De Muyter <phdm@info.ulb.ac.be\>
    *   "sz -" should work again. This will not work if sz cannot read from stdout.
    *   portability enhancements by Philippe De Muyter <phdm@info.ulb.ac.be\>
*   Version 0.12.9 - September 1996
    *   New options --min-bps N and --min-bps-time M: If BPS rate falls under N for at least M seconds (default: 120) transmission will be stopped.
    *   added some missing error messages.
    *   updated manual pages.
*   Version 0.12.8 - August 1996
    *   sz and rz now know about a new option: -E, --rename: change name if target exists.
    *   new option -T, --turbo for sz: sz doesn't escape 4 special characters if this option is given (this should not make problems with any rz, but could be problematic on certain links where this characters have to be escaped).
    *   debugged blocksize calculation.
    *   \-+, --append option fixed.

* * *

### Future developement

*   enhance portability.
*   use VMIN code some day (it's not hard to implement. it's hard to automagically check if VMIN works. It doesn't on older BSD versions).
*   make argv\[0\]-recognition of X/Y/Z-mode work with program\_name\_transform.
*   write a decent documentation.

* * *

### Comments

*   i will not say anything about the original unix zmodem sources. Just look at them and you'll know (even lrzsz is still worse than i like it to be).
*   the zmodem protocol is a pretty good example of a proprietary protocol:
    *   There are some proprietary, undocumented protocol extensions made by the original author. Furthermore they are implemented in such a way that nobody else can extend the protocol in a safe way.
    *   There is no way to get extensions included into the _standard_.
    *   The protocol is not too good designed. It's impossible to extend it in a safe way to transfer files in both directions.
    *   Security was not an issue to the author. The ability to let the receiver execute any command the sender tells him is nothing more then a really large security hole (as large as running older sendmail versions). Hackers dreams came true.
*   On the other hand it has some really good points - especially it is high efficient, and is, if implemented correctly, usable over a number of transmission channels nobody thought of at the time the protocol was designed.

* * *

Send comments to uwe@ohse.de.
