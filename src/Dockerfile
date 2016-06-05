FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y software-properties-common && apt-add-repository ppa:mjblenner/hal-flash && apt-add-repository multiverse && apt-get update && apt-get install -y firefox && apt-get install -y libhal1-flash && apt-get install -y ubuntu-restricted-extras && apt-get install -y openssh-server && apt-get install -y pulseaudio

RUN adduser --disabled-password --gecos "Firefox User" --uid 5001 firefox

# You need to add your ssh key to file id_rsa.pub so that you can access the container
RUN mkdir /home/firefox/.ssh
ADD id_rsa.pub /home/firefox/.ssh/authorized_keys
RUN chown -R firefox:firefox /home/firefox/.ssh

# Create OpenSSH privilege separation directory
RUN mkdir /var/run/sshd

RUN echo 'export PULSE_SERVER="tcp:localhost:64713"' >> /usr/local/bin/firefox-pulseaudio-forward    

RUN echo '/usr/bin/firefox --new-instance "$@"' >> /usr/local/bin/firefox-pulseaudio-forward
RUN chmod 755 /usr/local/bin/firefox-pulseaudio-forward

RUN mkdir -p /etc/adobe && echo "EnableLinuxHWVideoDecode=0" > /etc/adobe/mms.cfg

RUN mkdir /var/run/dbus

#ENTRYPOINT ["/usr/sbin/sshd", "-D"]
CMD dbus-daemon --system --fork && /usr/sbin/sshd -D

EXPOSE 22
