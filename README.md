<h2>Procedure to create a distributed Storm cluster(3 nodes) using Vagrant</h2><br>
0. Download Storm(http://www.apache.org/dyn/closer.lua/storm/apache-storm-1.0.2/apache-storm-1.0.2.tar.gz) and Zookeeper(http://ftp.wayne.edu/apache/zookeeper/current/zookeeper-3.4.9.tar.gz)<br>
1. Setup Vagrant to create 3 VMs<br>
2. Setup Zookeeper on the 3 machines<br>
3. Setup Storm on the 3 machines<br>
4. Start ZK + Storm<br>

<h3>1. Vagrant</h3><br>
- Vagrantfile describes the setting up of 3 machines with a private network<br>
- Use the command 'vagrant up' in this directory to start the VMs<br>
- Use 'vagrant ssh machine_name' to ssh into the respective VMs described in the file Vagrantfile<br>

<h3>2. Steps for setting up a multi-node Zookeeper ensemble [Check zoo.cfg included in this repo]</h3><br>
- Download the Zookeeper release, untar zookeeper on each of the VMs and setup a data directory called ~/zkData and other params in
  conf/zoo.cfg , setup 'server.1/2/3' with IPs of the Vagrant VMs<br>
- Create new dataDir in the location mentioned in zoo.cfg<br>
- echo 1/2/3 to the file dataDir/myid on respective VMs<br>
- Start zookeeper( sudo zkServer.sh start ) on all VMs and test if it is working<br>

Reference
- https://objectpartners.com/2014/05/06/setting-up-your-own-apache-kafka-cluster-with-vagrant-step-by-step/<br>
- https://www.vagrantup.com/docs/multi-machine/<br>
- http://www.thisprogrammingthing.com/2015/multiple-vagrant-vms-in-one-vagrantfile/<br>
- https://stash.ges.symantec.com/users/manoj_arya/repos/vagrant-hadoop-hbase-psuedo-distributed/browse<br>
- http://zookeeper.apache.org/doc/r3.3.3/zookeeperAdmin.html<br>
- http://www.ibm.com/developerworks/library/bd-zookeeper/<br>


<h3>3. Steps for multi-node Storm setup [Check storm.yaml included in this repo]</h3><br>
- Download Storm release, untar storm folder at ~<br>
- Create data dir  ~/stormData<br>
- Update storm.yaml<br>
  a. Update ZK servers with the 3 IPs of the VMs<br>
  b. Update Nimbus seeds(hosts) with the master server IP<br>
  c. Update storm dir with ~/stormData<br>
- Run 'bin/storm nimbus' on master, 'bin/storm supervisor' on workers and 'bin/storm ui' on master<br>
- Access UI through http://192.168.33.10:8080 on Windows/OSX host<br>

Reference
- Storm Applied book<br>
- http://storm.apache.org/releases/current/Setting-up-a-Storm-cluster.html<br>
