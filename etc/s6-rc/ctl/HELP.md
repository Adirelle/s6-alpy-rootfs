Usage
-----
	s6ctl [-v verbosity] [-l live] [-c compiled] [-s source] command [args]

Options
-------

-v verbosity
	Set the verbosity of s6-rc commands.
-l live
	Set the path to s6-rc live directory.
-c compiled
	Set the path to a symlink that points to the current compiled directory.
-s source
	Set the path to the service definition directoty.

Commands
--------

start names...
	Alias to s6-rc -u change names...
	
stop names...
	Alias to s6-rc -d change names...

restart names...
	Stop all named services then start them all again.
	
status [-d] [names...]
	Display the status of the selected services or bundles.
	Without a name, select all services.
	With -d, select the dependencies as well.
	Bundles are expanded to their atomic services.
	Call s6-svstat on service directoy of longruns.
	Check the status of oneshots using s6-rc -a list.

poweroff
	Alias to s6-poweoff.

reboot
	Alias to s6-reboot.

update
	Recompile the source and update the running database.

mkbundle name [contents...]
	Create a new bundle with the given contents.

mklongrun [-d dep1,dep2,...] name
	Create a new longrun with the given dependencies and empty run script.

mkoneshot [-d dep1,dep2,...] name
	Create a new oneshot with the given dependencies and empty up and down scripts.

mklogsvc [-d dep1,dep2,...] name
	Create a couple of longruns:
	1. The first is named "name-svc" and depends on deps1,deps2, etc...
	2. The second is named "name-log", depends on "localfs" and call "/etc/s6-rc
	Both are linked with a pipeline named "name".

help
	Prints this help.

Configuration
-------------

s6ctl also reads default configuration from /etc/s6-init/env and \$HOME/.s6ctl-env
directories, when they exist.

S6_VERBOSITY
	Verbosity of s6-rc commands.
	Default: 0

S6_LIVE
	Path to s6-rc live directory.
	Default: /run/s6-rc

S6_COMPILED
	Set the path to a symlink that points to the current compiled directory.
	Default: /etc/s6-rc/compiled

S6_SOURCE
	Set the path to the service definition directoty.
	Default: /etc/s6-rc/source
