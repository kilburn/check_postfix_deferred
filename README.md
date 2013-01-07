Nagios plugin to check postfix's deferred queue size
====================================================

This is a small nagios plugin to check the size of the deferred queue of a
remote postfix server.

Theory of operation
-------------------

The script connects through ssh to the remote box (key-based access required,
more details below). Then, it counts the number of files in the deferred queue,
assuming it is located in the _/var/spool/postfix/deferred/_ folder.

Requirements
------------

On the local box:
 * A properly working `nagios` instance.
 * An ssh rsa or dsa key installed in the `.ssh` folder of the user under which
   nagios user is running (usually _nagios_).
 * An initial ssh connection from this user to the remote box, so that the public
   key of the remote box gets stored within the nagio's user `.ssh/known_hosts`
   file.

On the remote box:
 * A user to which the local (monitoring) box can connect using its key.
 * Passwordless sudo rights for this user to run the "find" utility (warning: this
   gives effective root permissions to that user. Please do not re-use any existing
   user for that task).
