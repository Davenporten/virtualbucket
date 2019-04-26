# VirtualBucket
The purpose of *virtualbucket* is to have a modular way of turning on or off different services/tools/apps without impacting the overall system. Basically it is [virtualenv](https://github.com/pypa/virtualenv), running tools in an isolated environment, but allowing you to still have access to all other tools and functionality on your machine. For example, for some reason you couldn't install python3 globally onto your machine, but needed to work with some other tool that is on the machine, you could activate virtualbucket with python3 installed, using python3 as if it were installed on your machine, then deactivate it, without your system being effected. Once a bucket is build there is no need for installing anything on the machine that it is run on, you can just activate it and start using the tools. **Note**: this has only been tested on Ubuntu 16.04 and CentOS 7.5, it most likely will not work on non-Linux machines.

## Using VirtualBucket
VirtualBucket does two things: 1) creates buckets, and 2) runs buckets, giving you access to whatever tools you included when you created the bucket.

### Creating Buckets
This should be done on your home machine, where you have internet access and the ability to install whatever you want. You can create a bucket on your home machine and also run the bucket it there, but these steps will not work and are not meant to be run on a machine that does not have these capabilities.

The following steps should be run inside of the virtualbucket dir and you will need sudo privileges.

Steps:

1. Add what you'd like to be installed in the bucket to proto_config. The name of each package should be on it's own line and appear as it would if you were installing it using pip. 'django' is already in there as an example, feel free to remove it.

2. Run:

  $ source vb_setup

3. Go to wherever you'd like to create your bucket and run

  $ vb_build &lt;bucket_name&gt;

4. From here you can use the bucket you've create locally or package it to move it somewhere else

From here you can use the bucket you've created locally or create a tarball of it to move it somewhere else by running:

  $ vb_tarup &lt;bucket_name&gt;

### Use Bucket
These steps can be followed if you are using the bucket on your home machine or somewhere else, unless otherwise specified.

  $ cd &lt;bucket_name&gt;

If you are running on a machine that is NOT your home machine you will need to run

  $ source setup

Activate the bucket:

  $ source activate

You can then use the tools the bucket provides anywhere on your machine.

Deactivate the bucket (this can be called anywhere in your machine):

  $ source deactivate

If you would like to remove anything that setup created run

  $ source remove

**Note**: Below is not complete and needs to be updated.
## Explanation of Files
Any file with the prefix *proto_* will be files that are customized for a given build of virtualbucket, or changed in some other way to the system. *vb_* prefix means it will not be changed, but moved to a global location like /usr/bin/ for the user to have whenever. The proto_ prefix will not be present in buckets that were build by a user.

* setup

   Creates all needed dirs, files, and places needed scripts in a global scope. Should be the first thing that's run.
* proto_activate

   Sets the VB_ACTIVE variable to true, saves the current PATH of the machine, and set a new PATH for using virtualbucket based off of where the bucket is located in the file system.
* proto_config

   Tells vb what packages should be installed for a given bucket at the time of vb_build being run.
* proto_deactivate

   Sets the VB_ACTIVE variable to false, resets PATH to the saved PATH from proto_activate.
* proto_ev.sh

   To be placed in /etc/profile.d/virtualbox/, creates all needed environment variables.
* vb_build

   Based off of the current configuration will create a dir (bucket) that can be activated, deactivated, etc.
* vb_config

   Starts an ncurses UI where the user can set what will be included in a given bucket.
* vb_remove

   Removes all files and scripts created and placed by proto_setup. Will not work if vb is active.
* vb_tarup

   With the name of a given bucket passed to it this will create a .tar.gz with the entire bucket inside. It can then be moved to wherever the user needs it, even to another machine.
