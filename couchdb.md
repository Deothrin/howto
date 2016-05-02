**VirtualBox Setup**

After playing with couch on windows I wanted to connect to it from a virtualbox ubuntu guest. My first attempt was to change
the bind address for the couchdb server from 127.0.0.1 to 0.0.0.0 in the default.ini file. This may have worked (I don't remember)
but before that I discovered that norton was blocking connections from the guest to the host. Turning off the firewall at
least let me ping the host. To get norton to let traffic thru I added a new firewall rule for tcp and udp connections to allow traffic
between all machines on the virtualbox host network. Now I could ping with the firewall on. I decided to put couch back to listening
on localhost only and instead to setup an apache server to proxy requests from the host network to the couch server running on localhost.

To make this work I set apache to listen on 127.0.0.1:80 and 192.168.56.1:80 as well as 192.168.56.1:5984 and created virtual host
entries for each of these. The first two I pointed to different document roots and confirmed that they delivered different indexes.
The last virtualhost I configured with a ProxyPass from / to http://localhost:5984.
