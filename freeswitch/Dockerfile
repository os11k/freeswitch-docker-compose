FROM debian:stretch

COPY ./modules.conf /modules.conf

RUN apt-get update && \
apt-get -y install gnupg2 wget lsb-release && \
wget -O - https://files.freeswitch.org/repo/deb/debian-release/fsstretch-archive-keyring.asc | apt-key add - && \
echo "deb http://files.freeswitch.org/repo/deb/debian-release/ `lsb_release -sc` main" > /etc/apt/sources.list.d/freeswitch.list && \
echo "deb-src http://files.freeswitch.org/repo/deb/debian-release/ `lsb_release -sc` main" >> /etc/apt/sources.list.d/freeswitch.list && \
apt-get update && \
apt-get -y build-dep freeswitch && \
\
cd /usr/src/ && \
git clone https://github.com/signalwire/freeswitch.git -bv1.8 freeswitch && \
cd freeswitch && \
git config pull.rebase true && \
#Here you can build your Freeswitch on specific commit, it is allways good practice to do so
#git checkout 6047ebddfcb06c131a91f329e86fc8efba3e9e31 && \
cp /modules.conf /usr/src/freeswitch/modules.conf && \
\
./bootstrap.sh -j && \
./configure && \
make && \
make install

CMD ["/usr/local/freeswitch/bin/freeswitch", "-nonat"]

