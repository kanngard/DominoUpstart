# Domino Upstart Job

Tested with Domino 9.0.1 and Ubuntu 14.04 LTS. It might need some tweaking for older versions of Domino since the default locations for the binaries and data directories have changed.


# Installation

Clone the git repository and copy the necesarry files:

    cd ~
    git clone https://github.com/kanngard/DominoUpstart.git
    sudo cp DominoUpstart/src/etc/init/domino*.conf /etc/init
    sudo cp DominoUpstart/src/etc/domino/server1.conf.example /etc/domino

Rename the /etc/domino/server1.conf.example into a better name, preferrably the name of the Domino server. I e if the Domino server is named MyProdServer1/Acme, you might rename the file to myprodserver1_acme.conf. Open up this file and change the INSTANCE_NAME variable to the same name, which is used for logging into /var/log/domino_<INSTANCE_NAME>.log
If you have a password on your Domino server ID file (of course you have :-), you should add it in the data directory with the name .domino.pwd and make it readable only to the user running Domino:
   
    sudo echo mysecretpassword >> /local/notesdata/.domino.pwd
    sudo chmod 0400 /local/notesdata/.domino.pwd
    sudo chown dominouser:dominogroup /local/notesdata/.domino.pwd

Reload upstart config:

    sudo initctl reload-configuration

Check that Domino has been configured:

    sudo initctl list | grep domino

Done!


# Upstart Control

The commands to control upstart services are start, stop and restart.

Start all Domino instances:

    sudo start dominoall

Stop all Domino instances:

    sudo stop dominoall

Stop all Domino instances and then starts them:

    sudo restart dominoall

Start the Domino instance with the specified name:

    sudo start domino NAME=<servername>

Stop the Domino instance with the specified name:

    sudo stop domino NAME=<servername>

Stop and then start the specified Domino instance:

    sudo restart domino NAME=<servername>


# Add a new instance

If you have a partitioned Domino server with multiple Domino servers and separate data directories, you can copy the /src/etc/domino/server1.conf.example file into /etc/domino and rename it and change the INSTANCE_NAME and DATA_LOCATION variables.


# TODO
* Installation script