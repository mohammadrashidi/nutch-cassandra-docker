####Apache Nutch 2.x with Cassandra on Docker
=======================

This project is 3 Docker containers running Apache Nutch 2.x configured with Cassandra storage.

Due to the lack of integration information between Nutch 2.x / Cassandra, I have created this docker containers with configuration and integration between them.

This is project is fully operational but its still experimental, any feedback, suggestions or contribution will be highly appreciated! 

Current Nutch version is 2.3 ( There is a branch for 2.2.1 and it has ElasticSearch integrated since 2.3 missing elastic search indexerJob ).

###Usage notes:

1. Clone the repository.
2. Build the images and start the containers " NOTE: for Mac OS running boot2docker, Please read the Notes section Below ". 

```

# Build the images ( this will build the application )
./bin/build.sh

# Start all containers with data folders from scripts
./bin/start.sh

# stop all containers 
./bin/stop.sh

# restart containers 
./bin/stop.sh

```
3. Start Crawling with Nutch 2.2.


```
# Run the crawler, You can use docker exec command, or you can docker attach to the container and run the commands there, or use docker-enter if you are using Mac OS

docker exec NUTCH01 /opt/nutch/bin/crawl /opt/nutch/testUrls test_crawl 3
# OR

docker-enter NUTCH01
root@9ec43c388769:/# cd opt/nutch
root@9ec43c388769:/opt/nutch# ./bin/crawl
Usage: crawl <seedDir> <crawlID> [<solrUrl>] <numberOfRounds>
root@9ec43c388769:/opt/nutch# ./bin/crawl testUrls test_crawl 3


```
###NOTES:

Nutch 2.x Container name : NUTCH01

Cassandra Container name : CASS01

Cassandra installed with OpsCenter


###MAC OSx notes
- you need to mount data folders to your VirtualMachine to be able to get persistent data every time you run this application.
- You might need to install docker-enter for easier access to the containers

```
mkdir ~/docker-data
mkdir ~/docker-data/cassandra
mkdir ~/docker-data/nutch

chmod -R 777  ~/docker-data/

VBoxManage sharedfolder add boot2docker-vm -name home -hostpath ~/

boot2docker up
boot2docker ssh

#mkdir /data
#mount -t vboxsf -o uid=1000,gid=50 data /data
#vi /etc/fstab
#data            /data           vboxsf   rw,nodev,relatime    0 0
#docker-enter
```
