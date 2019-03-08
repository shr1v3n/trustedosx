RFC (undefined)
n@mod.net

SYNOPSIS:

When authenticating to perform an administrative task, on a asystem using least-privilege
for normal users, typically one user is able to modify all system preferences.

This is sub-optimal.  It means that whoever compromises the 'adm' account has compromised the
machine.

TARGETS:

This is applicable to all Unix/Linux operating systems, with the primary prototype being 
hardenedXNU / OS X.  HardenedXNU is our personal port of MachBSD and HardenedBSD packages.

WHAT ABOUT VULNERABILITIES IN HARDENEDBSD?  THEY DONT EXIST?

Of course they do, but with far less frequency than other implementations.
However, just last month FreeBSD and HardenedBSD's ELF image activators were fuzzed into
kernel panics by the author.

PROPOSAL:

Break the system operations, system preferences, and system policies (enforcement and creation/modification)
so that these operations are performed by the least-privileged role/user designed to do them.

ROLES:

Administrator roles:

wifiadm  -- tasked with wifi changes
netadm  -- tasked with networking changes
secadm  -- tasked with security changes
dispadm -- tasked with display changes
useradm -- tasked with creating unprivileged user 

These roles will be tagged in either struct cred or struct ecred/ucred.

procro -- ptrace(2) and procfs administration read-only (NO PTRACE_POKE, no open("/proc/.../mem", O_WRONLY|x);
procrw -- ptrace(2) and procfs administration read-write (PTRACE_PEEK/POKE and open("/proc/.../mem", O_RDWR);
fdadm -- watch, control, snoop, and read/write data directly for cloned filedescriptors
sockadm -- synonym for fdadm

DEFININING ROLES IN TRUSTED macOS:

Trusted MacOS will have configuration files in /tcb (Trusted Computing Base) which define role attributes.
There should be symlinks from /tcb/etc/roledefs.attr to /etc/roledefs.attr.

Format:

# WIFIADM bitmask 0x00000022
wifiadm:0x22:wifiadm,alladm





