## i2p-tor-rr

A round-robin load balancer between I2P and Tor to make the life of our friends at the NSA that much livelier.


### Prerequisites

Install [Vagrant](http://downloads.vagrantup.com/) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads).


### Usage

Clone the repository and run `vagrant up`. Once deployed instruct your browser to use **172.20.172.20:8118** as an HTTP and HTTPS proxy. Voilà. This uses [Privoxy](http://www.privoxy.org/) for cookie pruning and ad blocking. Should you like to use the I2P-Tor load balancer directly point your browser to use **172.20.172.20** on ports **8080** and **8090** for HTTP and HTTPS proxying, respectively.


### License

Simplified BSD. See the LICENSE file for details.