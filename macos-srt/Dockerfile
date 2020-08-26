FROM ubuntu:bionic
MAINTAINER Sergei Ovchinnikov (sovchinnikov@softvelum.com)
RUN	apt-get update -y
RUN	apt-get install wget gnupg sudo -y
RUN	wget -q -O - http://nimblestreamer.com/gpg.key | sudo apt-key add -
RUN	apt-get update -y
RUN	echo "deb http://nimblestreamer.com/ubuntu bionic/">>/etc/apt/sources.list \
	&& apt-get update -y
RUN	apt-get install nimble nimble-srt -y
ARG	wmspanel_account=install@wmspanel.com
ARG	WMSPANEL_PASS=q1w2e3ZXC
RUN	sudo /usr/bin/nimble_regutil -u $WMSPANEL_ACCOUNT -p $WMSPANEL_PASS --host dev.wmspanel.com

EXPOSE 8081 1935 554 4444-65535/udp
#ENTRYPOINT 	service nimble start 
ENTRYPOINT	/usr/bin/nimble -d --conf-dir=/etc/nimble --log-dir=/var/log/nimble --pidfile=/var/run/nimble/nimble.pid
