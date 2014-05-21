# Domino Upstart Job
Tested with Domino 9.0.1 and Ubuntu 14.04 LTS.

# Installation
FIXME rewrite to git clone into home directory and make an install script.

Copy /src/etc/init/dominoall.conf and /src/etc/init/domino.conf into /etc/init on the server.
Copy /src/etc/domino/server1.conf.example into /etc/domino and rename it to server1.conf (or usually the name of the Domino server)
Open the /etc/domino/server1.conf and change the INSTANCE_NAME variable into the same name.

To reload upstart config

    sudo initctl reload-configuration

To check that Domino has been configured

    sudo initctl list | grep domino

# Add a new instance
Copy the /src/etc/domino/server1.conf.example into /etc/domino and rename it and change the INSTANCE_NAME and DATA_LOCATION variables. This is often needed when a partitioned Domino server is used.

# Upstart Control
sudo start dominoall - starts all Domino instances
sudo stop dominoall - stops all Domino instances
sudo restart dominoall - stops all Domino instances and then starts them

sudo start domino <servername> - starts the Domino instance with the specified name
sudo stop domino <servername> - stops the Domino instance with the specified name
sudo restart domino <servername> - stops and then starts the specified Domino instance