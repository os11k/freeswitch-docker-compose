freeswitch-docker-compose
============

These are docker-compose files for building the 1.10 version of Freeswitch from source code.

I took modules.conf from the minimal configuration, and if you need to add any modules, you can add them there, just do not forget about the requirements and, of course, to load it afterwards by updating modules.conf.xml.

Keep in mind that this docker-compose is using the host network, so do not forget to firewall your system properly before putting this into production.

If your VPS is behind NAT (e.g. Amazon EC2), do not forget to set bind_server_ip, external_rtp_ip, and external_sip_ip as described here:

https://freeswitch.org/confluence/display/FREESWITCH/Amazon+EC2

Credits:
https://gist.github.com/cyrenity/96cc1ad7979b719b1c684f90aa0f526d

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
