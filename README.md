# mining-utils
This repository holds some useful scripts to optimize or automate mining operations.

# startup
This script is used to start mining scripts at startup and, if they fail, they can be automatically restarted.

The script is configured with a configuration file in the folder $HOME/.rig (which is the root directory for any other file).
* startup.cfg - *the main configuration file*
* logs/ - *the folder where logs are stored*
  * startupYYYYMMDD.log - *this is the format of the log files (a different one is created every day)*

**NOTE:** this script needs [screen](https://www.gnu.org/software/screen/) to be installed in order to work

## Configuration file

In the configuration file each semicolon-separated line represents a miner (or any other command) that has to be run.
The first value is the name of the screen window (no spaces or special character should be used, see the [screen manual](https://www.gnu.org/software/screen/manual/screen.html) for any particular limitation)
The second one is the script or even just a command that will be run, it can contain spaces but no semicolon. If the user needs to use semicolon, it is better to create a script and then put that in the configuration file
The last is the **enabled** value. If set to 1, the script will automatically run the command in case it stops running (it will also run it at startup), otherwise it will just ignore it. You can still run it manually though.

Here's an example of configuration file

    #this script will be run at startup and when it stops
    ETH;/home/user/bin/eth-miner.sh;1
    #this one wil not
    ETH;/home/user/bin/old-miner.sh;0

## Manual commands

This script can also be used manually. To do that, call the script with two arguments: the script name and the action. The allowed actions are:
* start
* stop
* enable - *will set the enable value to 1*
* disable - *will set the enable value to 0*

So, for example, to manually start the eth miner set before, just call in a terminal

    startup ETH start

Instead of the script name, you can also use a special identifier, currently there are two:
* all - *every script in the configuration file*
* all-enabled - *every script that is enabled*
