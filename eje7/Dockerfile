FROM ubuntu:latest
LABEL Daniel Cortés (dcortesf@uoc.edu)

RUN apt-get update -y && apt-get install openssh-server supervisor nginx -y

# Gestión de usuarios en el contenedor
RUN echo "root:password" | chpasswd
RUN useradd -rm -d /home/dcortesf -s /bin/bash -g root -G sudo -u 1000 dcortesf
RUN usermod -aG sudo dcortesf
RUN echo "dcortesf:password" | chpasswd

# sshd
RUN mkdir /root/.ssh
RUN mkdir /var/run/sshd
RUN chmod 777 /etc/ssh/sshd_config
RUN echo "PasswordAuthentication yes" >> /etc/ssh/sshd_config
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config 

# nginx
# configure nginx to serve static page
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN mkdir -p /var/www
#ADD nginx/default           /etc/nginx/sites-available/default
#ADD nginx/index.html        /var/www/index.html

# configure supervisor
RUN mkdir -p /var/log/supervisor
ADD supervisor/sshd.conf   /etc/supervisor/conf.d/sshd.conf
ADD supervisor/nginx.conf   /etc/supervisor/conf.d/nginx.conf

#clean-up
RUN apt-get clean

#RUN service ssh start
EXPOSE 22
EXPOSE 80

#CMD ["/usr/sbin/sshd","-D"]
CMD ["/usr/bin/supervisord", "-n"]