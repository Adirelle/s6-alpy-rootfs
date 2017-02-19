Usage
-----
	s6ctl [-v verbosity] [-l live] [-c compiled] [-s source] command [args]

Options
-------

* `-v verbosity` sets the verbosity level of s6-rc commands.
* `-l live` sets the path to s6-rc live directory.
* `-c compiled` sets the path to a symlink that points to the current compiled directory.
* `-s source` sets the path to the service definition directoty.

Commands
--------

##### s6ctl start name1 [name2 ...]

Alias to `s6-rc -u change name1 name2 ...`.

##### s6ctl stop name1 [name2 ...]

Alias to `s6-rc -d change name1 name2 ...`.

##### s6ctl restart name1 [name2 ...]

Stop all named services then start them all again.
	
##### s6ctl status [-d] [name1 [name2 ...]]

Display the status of the selected services or bundles.

  * Without any names, select all the services.
  * With `-d`, select the *dependencies* as well.
  * *Bundles* are expanded to their atomic services.
  * Call `s6-svstat` on service directoy of *longruns*.
  * Check the status of *oneshots* using `s6-rc -a list`.

##### s6ctl poweroff
	
Alias to `s6-poweoff`.

##### s6ctl reboot
	
Alias to `s6-reboot`.

##### s6ctl update
	
Recompile the source and update the running database.

##### s6ctl mkbundle name [contents...]
	
Create a new bundle with the given contents.

##### s6ctl mklongrun [-d dep1,dep2,...] name
	
Create a new longrun with the given dependencies and empty `run` script.

##### s6ctl mkoneshot [-d dep1,dep2,...] name

Create a new oneshot with the given dependencies and empty `up` and `down` scripts.

##### s6ctl mklogsvc [-d dep1,dep2,...] name
	
Create a couple of longruns:

1. The first is named `name-svc` and depends on `deps1`, `deps2`, etc...
2. The second is named `name-log`, depends on `localfs` and call `/etc/s6-rc/scripts/logger`.

Both are linked with a pipeline named `name`.

##### s6ctl help
	
Prints this help.

Configuration
-------------

s6ctl also reads default configuration from `/etc/s6-init/env` and `$HOME/.s6ctl-env`
directories, when they exist.

##### S6_VERBOSITY
	
Verbosity of s6-rc commands.

Default: `0`

##### S6_LIVE

Path to s6-rc live directory.

Default: `/run/s6-rc`

##### S6_COMPILED
	
Set the path to a symlink that points to the current compiled directory.

Default: `/etc/s6-rc/compiled`

##### S6_SOURCE
	
Set the path to the service definition directory.

Default: `/etc/s6-rc/source`
