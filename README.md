# openfire-vagrant-kerberos
A vagrant-based set of servers that instantiate an Openfire XMPP domain using Kerberos. Intended for SSO testing.

# Prerequisites
This project requires Ansible, Vagrant and Virtualbox.

To install the prerequisites using apt, execute:

    # apt-get install vagrant virtualbox ansible
    
Although any semi-recent versions should do, these versions are known to work (and are available with a standard Ubuntu 16.10 installation):

* ansible 2.1.1.0-1
* vagrant 1.8.5+dfsg-2
* virtualbox 5.1.6-dfsg-2

# Starting your environment

To create all servers, issue this from the directory in which you placed a copy of this repository:

    $ vagrant up

This will instantiate a number of servers. The domain name that is used is ```example.com````, which doubles as a Kerberos realm name (although there, it's typically references in all uppercase letters: ```EXAMPLE.COM```).

The servers that are created:

| Server name | Purpose                                                                      |
|-------------|------------------------------------------------------------------------------|
| bind01      | Provides a nameserver for the other hosts, used to serve up the DNS records. | 
| openfire01  | Runs a version of Openfire.                                                  |
| kdc01       | Hosts a Kerberos Key Distribution Center.                                    |

After the servers are created, you can SSH into any one of them, by using the Vagrant SSH subcommand and the name of the server:

    $ vagrant ssh bind01
    
You'll not need to authenticate explicitly and ```sudo``` is available without a password too.

To shut down your servers, issue;

    $ vagrant halt
