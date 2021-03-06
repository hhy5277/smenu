.. image:: smenu.gif

What is it?
===========
**smenu** is a selection filter just like ``sed`` is an editing filter.

This simple tool reads words from the standard input, presents them in
a cool interactive window after the current line on the terminal and writes
the selected word, if any, on the standard output.

After having unsuccessfully searched the NET for what I wanted, I
decided to try to write my own.

I have tried hard to made its usage as simple as possible. It should
work, even when using an old ``vt100`` terminal and is ``UTF-8`` aware.

The wiki (https://github.com/p-gen/smenu/wiki) contains screenshots and
animations that detail some of the concepts and features of smenu.

How to build it?
================
**smenu** can be built on every system where a working ``terminfo``
development platform is available. This includes every Unix and Unix
like systems I am aware of.

Please use the provided ``build.sh`` to build the executable. This
script accepts the same arguments as ``configure``, type ``build.sh
--help`` to see them.

The script ``autogen.sh`` is also provided if you need to generate a
new ``configure`` script from ``configure.ac`` and ``Makefile.am``. The
GNU **autotools** will need to be installed for this script to work.

How to install it?
==================
Once the build process has finished, a simple ``make install`` with the
appropriate privileges will do it

Some examples.
==============

Linux example.
--------------
This program should work on most Unix but if you are using Linux,
try to type the following line at a shell prompt (here: ``"$ "`` ):

::

  $ R=$(grep Vm /proc/$$/status \
        | smenu -n20 -W $':\t\n' -q -c -b -g -s /VmH)
  $ echo $R

Something like this should now be displayed with the program waiting
for commands: (numbers are mine, yours will be different)

::

  VmPeak¦    23840 kB
  VmSize¦    23836 kB
  VmLck ¦        0 kB
  VmHWM ¦     2936 kB
  VmRSS ¦     2936 kB
  VmData¦     1316 kB
  VmStk ¦      136 kB
  VmExe ¦       28 kB
  VmLib ¦     3956 kB
  VmPTE ¦       64 kB
  VmSwap¦        0 kB

A cursor should be under ``"VmHWM "``.

After having moved the cursor to ``"      136 kB"`` and ended the program
with ``<Enter>``, the shell variable R should contain: ``"      136 kB"``.

.. raw:: pdf

  PageBreak

Unix example.
-------------
The following command, which is Unix brand agnostic, should give you a
scrolling window if you have more than 10 accounts on your Unix with a
UID lower than 100:

::

  $ R=$(awk -F: '$3 < 100 {print $1,$3,$4,$NF}' /etc/passwd \
        | smenu -n10 -c)
  $ echo $R

On mine (``LANG`` and ``LC_ALL`` set to ``POSIX``) it displays:

::

  at      25 25  /bin/bash      \
  sys     0  3   /usr/bin/ksh   +
  bin     1  1   /bin/bash      |
  daemon  2  2   /bin/bash      |
  ftp     40 49  /bin/bash      |
  games   12 100 /bin/bash      |
  lp      4  7   /bin/bash      |
  mail    8  12  /bin/false     |
  named   44 44  /bin/false     |
  ntp     74 108 /bin/false     v

Note the presence of a scrollbar.

Testing and reporting.
----------------------
The included testing system is relatively young, please be indulgent.

**IMPORTANT** the testing system has some dependencies, please read the
``test/README.rst`` before going further.

**WARNING** running all the test by running ``./tests.sh`` in the
``tests`` directory will take some time (around 15 min for now).

**NOTE** on some systems like \*BSD some tests may fail. This can be
explained by differences in posix/libc/... implementations.  This can
notably occur when some specific regular expressions or uncommon UTF-8
byte sequences are used.

If a test fails for unknown reason, then please send me its directory
name and the relevant ``.bad`` file.

If you are hit by a bug that no test covers, then you can create a new
test in the ``tests`` directory in a existing or new directory, read the
``tests/README.rst`` file, use an existing test as model, create an
``.in`` file and a ``.tst`` file and send them to me as well as the
produced files.

Interested?
-----------
Please use the included man page to learn more about this little program.
