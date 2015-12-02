title: Distributed Wordpress with CoreOS
date: 2015-12-02 12:26:30
tags:
 - coreos
 - wordpress
 - docker
 - vulcand
category: OS
---

[CoreOS](http://coreos.com) can seem daunting at first. This tutorial is built to encourage you in your journey and to demonstrate the power of this minimalistic operating system.

# Exercise 1: Boot up a 3 machine coreos cluster

## 1a: Install prerequisite software

* [Download & install Virtualbox](https://www.virtualbox.org/wiki/Downloads)
* [Download & install Vagrant](http://www.vagrantup.com/downloads.html)

## 1b: Clone the coreos-vagrant repo

```
mkdir ~/coreos; cd ~/coreos
git clone https://github.com/coreos/coreos-vagrant.git
```

## 1c: modify your config.rb

```
cd coreos-vagrant
cp config.rb.sample config.rb

vim config.rb
```

change $num_instances:

```
$num_instances=3
```

change $update_channel:

```
$update_channel=‘beta’
```

change $forwarded_ports:

```
$forwarded_ports = {8000 => 8888}
```

You'll see why later.

## 1d: get yourself a discovery token

Visit [https://discovery.etcd.io/new?size=3](https://discovery.etcd.io/new?size=3)

You'll need a new one every time you rebuild a cluster.

Copy the entire URL provided in the body of the response somewhere safe.

## 1e: modify your user-data and turn on etcd2

etcd2 is a complete reimplementation based on research and learning about Raft. While backwards compatibility exists, we'd be silly not to go for the latest and greatest.

Update coreos-vagrant/user-data by changing the following.

Set the reboot strategy on CoreOS update:

```
    update:
      reboot-strategy: etcd-lock
```

Disable etcd properties in favour of etcd2:

```
    #etcd:
    # addr: $public_ipv4:4001
    # peer-addr: $public_ipv4:7001
```

Add your discovery token from 1D (warning: you need to do this each time):

```
    discovery: https://discovery.etcd.io/YOUR_DISCOVERY_TOKEN_HERE_FROM_1D
```

Stop etcd.service from starting in favour of etcd2:

```
      #- name: etcd.service
      #  command: start
```

Enable etcd2:

```
    - name: etcd2.service
      command: start
```

## 1f: magic

In the coreos-vagrant directory run:

```
    vagrant up
    vagrant status
```

Within a few minutes, you'll have 3 CoreOS machines, ready to go all based on the beta channel.

# Exercise 2: Interact with your cluster

## 2a: Download fleetctl

* Download [https://github.com/coreos/fleet/releases](https://github.com/coreos/fleet/releases
)

* Unzip to an appropriate location, add the binary to your path (.bashrc / .bash_profile / .zshrc)

```
    PATH=$PATH:/path/to/fleetctl
```

* Restart your terminal

## 2b: Start your engines

```
    cd /path/to/coreos-vagrant
    eval $(ssh-agent)
```

Add the correct vagrant .ssh identify

```
    vagrant ssh-config | sed -n "s/IdentityFile//gp" | uniq | xargs ssh-add
```

## 2c: Get ready for fleet

```
    export FLEETCTL_TUNNEL="127.0.0.1:$(vagrant ssh-config | grep -i 'port' | awk '{print $2; exit}')"
```

### Remove your fleet known hosts

Fortunately there is a specific known_hosts file to clean up. Do this after every cluster rebuild.

```
    rm ~/.fleetctl/known_hosts
```

## 2e: List your machines via fleet

You should see your 3 CoreOS machines listed.

```
    fleetctl list-machines
```

SSH onto one of your CoreOS hosts. `exit` when done.

```
    fleetctl ssh (machine-id)
```

# Exercise 3: Use CoreOS with scale

## 3a: Initial setup and play

```
    mkdir ~/coreos; cd ~/coreos
```

Download some sample unit files:

```
    git clone git@github.com:shaundomingo/coreos-units.git
```

### Hello unit

Submit the hello unit and watch the containers say hello.

```
    cd ~/coreos/coreos-units/hello

    fleetctl submit hello.service; fleetctl start hello.service

    fleetctl journal -f hello.service
```

Once you're done greeting yourself, stop the unit and destroy it.

```
    fleetctl destroy hello.service
```

## 3b: Deploy at scale - add config

Hello worlds suck. Let's deploy something that's interesting with scale!

Let's fire up lots of Wordpress instances. We won't go into detail in this tutorial, but this is what we'll build (minus the top Load Balancer - but expect it's easy).

```
                            +---------80----------+                        
                            |                     |                        
                            |    Load Balancer    |                        
                            |                     |                        
                            +--------8888---------+                        
                          /            |            \                      
                         /             |             \                     
    +-------8888---------+   +--------8888--------+  +-------8888---------+
    |                    |   |                    |  |                    |
    |      core-01       |   |       core-02      |  |      core-03       |
    |                    |   |                    |  |                    |
    +--------------------+   +--------------------+  +--------------------+
    |      vulcand       |   |       vulcand      |  |      vulcand       |
    +--------------------+   +--------------------+  +--------------------+
    | discovery sidekick |   | discovery sidekick |  | discovery sidekick |
    +--------------------+---+--------------------+--+--------------------+
    | wp wp wp wp wp wpn |   | wp wp wp wp wp wpn |  | wp wp wp wp wp wpn |
    +--------------------+   +--------------------+  +--------------------+
```

NOTE: The wp instances will talk through to a single database server. While databases on CoreOS and containers is entirely possible, and done, I prefer to exclude the database from this setup. Set yourself up with a VM, install mariadb (/mysql) and follow the [wordpress database installation instructions](https://codex.wordpress.org/Installing_WordPress#Using_the_MySQL_Client).

### Edit the unit files for wordpress@.service and wordpress-admin.service.

Edit wordpress@.service ...

```
    vim coreos-units/clusterable-wordpress/wordpress/wordpress@.service
```

... and change line 12 to incorporate your database and S3 creds:

```
    ExecStart=/usr/bin/docker run -rm --name wordpress-%i -e WORDPRESS_DB_NAME=dbname -e WORDPRESS_DB_HOST=dbhost:dbport -e WORDPRESS_DB_USER=dbuser -e WORDPRESS_DB_PASSWORD=dbpassword -e WORDPRESS_CACHE_S3_KEY=s3key -e WORDPRESS_CACHE_S3_SECRET=s3secret -e WORDPRESS_CACHE_S3_BUCKET=s3bucket -e WORDPRESS_CACHE_HOME="http://wordpress.local:8888" -p 80 sdomsta/clusterable-wordpress
```

Edit wordpress-admin.service ...

```
  vim coreos-units/clusterable-wordpress/wordpress/wordpress-admin.service
```

... and change line 12 to this (only difference is this: -e WORDPRESS_ADMIN_ENABLED=true):

```
    ExecStart=/usr/bin/docker run -rm --name wordpress-%i -e WORDPRESS_DB_NAME=dbname -e WORDPRESS_DB_HOST=dbhost:dbport -e WORDPRESS_DB_USER=dbuser -e WORDPRESS_DB_PASSWORD=dbpassword -e WORDPRESS_CACHE_S3_KEY=s3key -e WORDPRESS_CACHE_S3_SECRET=s3secret -e WORDPRESS_CACHE_S3_BUCKET=s3bucket -e WORDPRESS_CACHE_HOME="http://wordpress.local:8888" -e WORDPRESS_ADMIN_ENABLED=true -p 80 sdomsta/clusterable-wordpress
```

## 3c: Run up your cluster

Either follow clusterable-wordpress/README.md for instructions on how to run, or if you’re like me and like to cheat:

```
    cd ~/coreos/coreos-units/clusterable-wordpress
    ./wordpress-up.sh
```

## 3d: Observe your mighty cluster firing up

The cluster deploys the following:

1. A discovery sidekick unit that watches for wordpress units that start and get destroyed. This particular unit is unique in that it can detect the type of wordpress container firing up, and configures the vulcand locations and paths as required.
2. [vulcand](https://github.com/mailgun/vulcand), a "programmatic load balancer backed by etcd" that listens for etcd entries and reconfigures itself instantly as config changes.
3. wpadmin (the wordpress control panel) as a separate container. After much trial and error vulcand doesn't support sticky session persistence and wp-admin isn't written to deal with sessions moving all over the place.
4. customised wordpress containers, using the [w3 total cache](https://wordpress.org/plugins/w3-total-cache/) plugin, with wp-admin disabled by a custom .htaccess denying access.

The vulcan@.service, wordpress@.service and wordpress.service units all depend on docker images, which take a while to download the first time. As your cluster fires up watch the status of all units until all are up and running:

```
    fleetctl list-units
```

Since you're firing these containers up at the same time, your containers may take some time to start and be in `running` state.

## 3e: Check and discover

```
    fleetctl journal -f discovery@1.service
    fleetctl journal -f wordpress@1.service
    fleetctl journal -f wordpress-admin.service
```

Ctrl+c at any time.

## 3f: Play with your brand new wordpress site

Add an entry to your hostfile:

```
    sudo vim /etc/hosts
```

Add the following line:

```
    127.0.0.1 wordpress.local
```

Note, you must call the host `wordpress.local` because this is the value configured in our sample wordpress database.

*And finally*... click on this magic link:

[http://wordpress.local:8888](http://wordpress.local:8888)

Refresh the page over and over again and watch the container id change.

## 3g: clean up

Oh, don't forget to shut everything down! Repeat until everything is destroyed:

```
    fleetctl destroy (name)(@number).service
    fleetctl list-units
```

If you don't want this coreos cluster anymore, just blow it away (in fact you don't really have to manually clean up each unit, as above ... just destroy your CoreOS cluster)!

```
    cd ~/coreos/coreos-vagrant
    vagrant destroy
```

# Celebrate good times
You've deployed a scalable Wordpress site.

Grab yourself some french toast, paw paw juice and toffee apple and chill out in celebration.

If you need some help with CoreOS, ping me on [twitter](http://twitter.com/sdomsta). I think this OS brings great promise and I'm keen to understand how you'll use it.