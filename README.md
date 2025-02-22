# Freeswitch Docker Compose

These are Docker Compose files for building Freeswitch 1.10 from source.

I took `modules.conf` from the minimal configuration. If you need to add any modules, you can do so there—just remember the requirements and to load them afterward by updating `modules.conf.xml`.

Keep in mind that this setup uses the host network, so ensure your system is properly firewalled before putting it into production.

## Configuration for NAT (e.g., Amazon EC2)

If your VPS is behind NAT, update the following files:

### Update `freeswitch/Dockerfile`
```diff
-CMD ["/usr/local/freeswitch/bin/freeswitch", "-nonat"]
+CMD ["/usr/local/freeswitch/bin/freeswitch"]
```

### Update `freeswitch/conf/vars.xml`
```diff
+  <X-PRE-PROCESS cmd="set" data="bind_server_ip=YOUR-EXTERNAL-IP"/>
+  <X-PRE-PROCESS cmd="set" data="external_rtp_ip=YOUR-EXTERNAL-IP"/>
+  <X-PRE-PROCESS cmd="set" data="external_sip_ip=YOUR-EXTERNAL-IP"/>
```

For more details, refer to the official documentation:
[Amazon EC2 - FreeSWITCH](https://freeswitch.org/confluence/display/FREESWITCH/Amazon+EC2)

## Usage

```sh
apt-get update && apt-get upgrade -y && apt-get install docker-compose -y
cd /usr/src
git clone https://github.com/os11k/freeswitch-docker-compose.git
git clone https://github.com/signalwire/freeswitch.git
cp -a ./freeswitch/conf/minimal ./freeswitch-docker-compose/freeswitch/conf
cd ./freeswitch-docker-compose/
docker-compose up -d --build
```

## Credits

Based on a guide by [cyrenity](https://gist.github.com/cyrenity/96cc1ad7979b719b1c684f90aa0f526d).

