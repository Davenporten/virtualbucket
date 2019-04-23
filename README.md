# virtualbucket
The purpose of *virtualbucket* is to have a modular way of turning on or off different services/tools/apps without impacting the overall system. Basically it is [virtualenv](https://github.com/pypa/virtualenv), running tools in an isolated environment, but allowing you to still have access to all other tools and functionality on your machine. For example, for some reason you couldn't install python3 globally onto your machine, but needed to work with some other tool that is on the machine, you could activate virtualbucket with python3 installed, using python3 as if it were installed on your machine, then deactivate it, without your system being effected.

## Explanation of Files
Any file with the prefix *proto_* will be files that are customized for a given build of virtualbucket, or changed in some other way to the system. *vb_* prefix means it will not be changed, but moved to a global location like /usr/bin/ for the user to have whenever. The proto_ prefix will not be present in buckets that were build by a user.

..* proto_activate
Sets the VB_ACTIVE variable to true, saves the current PATH of the machine, and set a new PATH for using virtualbucket based off of where the bucket is located in the file system.
..* proto_config
Tells vb what packages should be installed for a given bucket at the time of vb_build being run.
..* proto_deactivate
Sets the VB_ACTIVE variable to false, resets PATH to the saved PATH from proto_activate.
..* proto_ev.sh
To be placed in /etc/profile.d/virtualbox/, creates all needed environment variables.
..* proto_remove
Removes all files and scripts created and placed by proto_setup. Will not work if vb is active.
..* proto_setup
Creates all needed dirs, files, and places needed scripts in a global scope.
..* vb_build
Based off of the current configuration will create a dir (bucket) that can be activated, deactivated, etc.
..* vb_config
Starts an ncurses UI where the user can set what will be included in a given bucket.
..* vb_tarup
With the name of a given bucket passed to it this will create a .tar.gz with the entire bucket inside. It can then be moved to wherever the user needs it, even to another machine.
