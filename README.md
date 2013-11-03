# NAME

fakechroot - gives a fake chroot environment

# SYNOPSIS

__fakechroot__
\[__\-s__|__\--use-system-libs__\]
\[__\-l__|__\--lib__&nbsp;_library_\]
\[__\-e__|__\--environment__&nbsp;_type_\]
\[__\-c__|__\--config-dir__&nbsp;_directory_\]
\[__\--__\]
\[_command_\]

__fakechroot__
\[__\-h__|__\--help__\]

__fakechroot__
\[__\-v__|__\--version__\]

# DESCRIPTION

fakechroot runs a command in an environment were is additional possibility to
use chroot(8) command without root privileges.  This is useful for allowing
users to create own chrooted environment with possibility to install another
packages without need for root privileges.

fakechroot replaces more library functions (chroot(2), open(2), etc.) by ones
that simulate the effect the real library functions would have had, had the
user really been in chroot.  These wrapper functions are in a shared library
`/usr/lib/fakechroot/libfakechroot.so` which is loaded through the
`LD_PRELOAD` mechanism of the dynamic loader.  (See ld.so(8))

In fake chroot you can install Debian bootstrap with debootstrap(8)
command.  In this environment you can use i.e. apt-get(8) command to install
another packages from common user's account.

In the current version, the fakechroot does not provide the fakeroot(1)
functionality! You might to call fakechroot with fakeroot command, if you
want to emulate root environment, i.e.:

    $ fakechroot fakeroot /usr/sbin/chroot /tmp/debian /bin/sh
    # id
    uid=0(root) gid=0(root) groups=0(root)

# SECURITY ASPECTS

fakechroot is a regular, non-setuid program.  It does not enhance a user's
privileges, or decrease the host's system security.

fakechroot should not be used as a tool for enhancing system security i.e. by
separating (sandboxing) applications.  It is very easy to escape from a fake
chroot environment.

# BUGS

If you find the bug or want to implement new features, please report it at
[https://github.com/fakechroot/fakechroot/issues](https://github.com/fakechroot/fakechroot/issues)

# AUTHORS

Copyright (c) 2003, 2005, 2007-2011, 2013 Piotr Roszatycki <dexter@debian.org>

Copyright (c) 2007 Mark Eichin <eichin@metacarta.com>

Copyright (c) 2006, 2007 Alexander Shishkin <virtuoso@slind.org>

Copyright (c) 2006, 2007 Lionel Tricon <lionel.tricon@free.fr>

# COPYING

fakechroot is distributed under the GNU Lesser General Public License (LGPL
2.1 or greater).
