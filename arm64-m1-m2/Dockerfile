FROM ubuntu:focal
MAINTAINER Sergei Ovchinnikov (https://wmspanel.com/help)
LABEL    description="Nimble Streamer with SRT"

RUN    apt-get update -y
RUN    apt-get install wget gnupg sudo vim less -y

ENV    TZ=Asia/Vladivostok
RUN    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN    wget -q -O - http://nimblestreamer.com/gpg.key | sudo apt-key add -
RUN    apt-get update -y
RUN    echo "deb http://nimblestreamer.com/raspbian/ buster/" >> /etc/apt/sources.list
RUN    echo "deb http://us-east-2.ec2.ports.ubuntu.com/ubuntu-ports/ bionic universe" >> /etc/apt/sources.list
RUN    apt-get update -y
RUN    apt-get install nimble nimble-srt nimble-transcoder -y

ARG    WMSPANEL_SERVER_NAME=SRT-MACOS
ARG    WMSPANEL_ACCOUNT=
ARG    WMSPANEL_PASS=
ARG    WMSPANEL_TRANSCODER_LICENSE=

RUN    sudo /usr/bin/nimble_regutil -u $WMSPANEL_ACCOUNT -p $WMSPANEL_PASS --server-name $WMSPANEL_SERVER_NAME --host nimble.wmspanel.com
RUN    sudo /usr/bin/nimble_regutil -u $WMSPANEL_ACCOUNT -p $WMSPANEL_PASS --transcoder-license $WMSPANEL_TRANSCODER_LICENSE --host nimble.wmspanel.com

RUN    sudo echo "management_listen_interfaces = *" >> /etc/nimble/nimble.conf 

#EXPOSE 8081 1935 554 4444/udp
ENTRYPOINT    ["/usr/bin/nimble", "--conf-dir=/etc/nimble", "--log-dir=/var/log/nimble","--pidfile=/var/run/nimble/nimble.pid"]
