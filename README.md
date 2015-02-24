###### MongoDB 

* [install MongoDB](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-red-hat-centos-or-fedora-linux/) to Cent OS 7.x and disable service for now
```
$ sudo yum install mongodb-server
$ sudo systemctl disable mongod mongos
$ sudo yum-config-manager --add-repo=http://downloads-distro.mongodb.org/repo/redhat/os/x86_64 --disable --nogpgcheck
$ sudo yum repolist all | grep mongodb
downloads-distro.mongodb.org_repo_redhat_os_x86_64 added from: ht enabled:   250
$ sudo yum install --enablerepo='downloads-distro.mongodb.org_repo_redhat_os_x86_64' -y \
 mongodb-org mongodb-org-server mongodb-org-shell mongodb-org-mongos mongodb-org-tools
```
* dealing with selinux. disable it first. or allow port listening on 27017
```
$ getenforce
Disabled

$ sudo semanage port -a -t mongod_port_t -p tcp 27017
```
* starting service
```
$ sudo systemctl start mongod
$ sudo systemctl status mongod -l

bigchoo@vmk2 1003 $ sudo journalctl -xn
-- Logs begin at Mon 2015-02-23 17:20:44 PST, end at Tue 2015-02-24 02:12:53 PST. --
Feb 24 02:10:36 vmk2.cracker.org systemd[1]: Starting SYSV: Mongo is a scalable, document-oriented database....
-- Subject: Unit mongod.service has begun with start-up
-- Defined-By: systemd
-- Support: http://lists.freedesktop.org/mailman/listinfo/systemd-devel
--
-- Unit mongod.service has begun starting up.

bigchoo@vmk2 1005 $ sudo tail -f /var/log/mongodb/mongod.log
2015-02-24T02:10:38.440-0800 [initandlisten] waiting for connections on port 27017
2015-02-24T02:11:37.768-0800 [clientcursormon] mem (MB) res:32 virt:443
2015-02-24T02:11:37.769-0800 [clientcursormon]  mapped (incl journal view):160
2015-02-24T02:11:37.769-0800 [clientcursormon]  connections:0
```
* review configuration [/etc/mongod.conf](http://docs.mongodb.org/manual/reference/configuration-options/)
* review Chef recipe [mongodb](https://supermarket.chef.io/cookbooks/mongodb#readme)
* review Nagios passive check plugin for [MongoDB monitoring](https://github.com/mzupan/nagios-plugin-mongodb)
* review metrics plugin for [MongoDB metrics plugin](https://collectd.org/wiki/index.php/Plugin:MongoDB)
* added two nodes. One for master and another for slave
```
```
