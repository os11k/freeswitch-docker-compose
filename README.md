freeswitch-docker-compose
============

This are docker-compose files for building 1.10 version of Freeswitch from sources.

If you need to build 1.8, just switch to 1.8 branch for this git repository, or change 1.10 to 1.8 and buster to stretch in Dockerfile.

I took modules.conf from minimal configuration and if you need to add any module you can add them there, just do not forget about requirements and off cause to load it after by updating modules.conf.xml.

Keep in mind that this docker-compose is using host network, so do not forget to firewall your system properly before putting this to production.

If your VPS is behind NAT(Amazon EC2 for example), do not forget to set bind_server_ip, external_rtp_ip, external_sip_ip as described here:

https://freeswitch.org/confluence/display/FREESWITCH/Amazon+EC2

### Usage
```
apt-get update && apt-get upgrade -y && apt-get install docker-compose -y
cd /usr/src
git clone https://github.com/os11k/freeswitch-docker-compose.git
git clone https://github.com/signalwire/freeswitch.git
cp -a ./freeswitch/conf/minimal ./freeswitch-docker-compose/freeswitch/conf
cd ./freeswitch-docker-compose/
#git checkout v1.8 # uncomment beginning of this line to build 1.8
docker-compose up -d --build
```
