# check_test
A monitoring plugin strictily for testing

While `check_dummy` fine for simple tests I needed a more sophisticated testing plugin. This works for Icinga (2) as well as every other tool using monitoring plugins like Shinken, Naemon, Nagios, etc.

Things which can not be done with `check_dummy` or `check_random` :

* Get several times an `OK` state and suddenly switching to `Critical` without restarting / reloading the monitoring software or injecting passive check results. Either by changing the configfile by hand or have it automatically change after a set amount of checks.
* Switch randomly between a predefined set of statuses
* Change state at a certain time (useful for testing planned downtimes)
* Change the state under certain controlled conditions and change it back later

## Disclaimer ##

This plugin is very simple at the moment. I will expand it's possibilities as I need more functionality while running tests. If you need special cases: Patches are welcome.

Monitoring plugins should not use external config files or temporary files but since this is not to be used in production environments it should be ok to use them anyway.

## Usage ##

Since the whole reason why I wanted this plugin was to be able to change the output whithout changing Icinga 2, it has only one commandline argument: Where to find a configuration file. This is what you change while Icinga 2 is running.

    sudo -u icinga ./check_test -f [configfile]

Keep in mind that you can set the file to use on a per check basis. This way you can create several test cases in one setup.

### Configuration file ###

The configuration file by now only supports setting the return code and the output of the plugin. More options are to come.

Example file:

    STATUS=2
    OUTPUT="Custom output"


## Acknowledgements ##

* This plugin was created for running some tests for the upcoming [Icinga 2](https://www.icinga.org/) 2.6 release
* I created this plugin as part of my work for [Netways](https://www.netways.de/home/)
