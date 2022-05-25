FROM ubuntu:latest
LABEL Daniel Cortés (dcortesf@uoc.edu)

RUN apt-get update -y && apt-get install openssh-server -y

RUN echo "root:password" | chpasswd
RUN useradd -rm -d /home/dcortesf -s /bin/bash -g root -G sudo -u 1000 dcortesf
RUN usermod -aG sudo dcortesf
RUN echo "dcortesf:password" | chpasswd
RUN mkdir /root/.ssh
RUN mkdir /var/run/sshd

RUN chmod 777 /etc/ssh/sshd_config
RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config 

RUN service ssh start
EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]