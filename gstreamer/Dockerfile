#
# IMRAD development env.
#

# Pull base image.
FROM menglj/docker-opencv

RUN apt-get -y update && apt-get -y install gstreamer1.0 gstreamer1.0-dev
RUN apt-get -y install git vim sudo openssh-server

#RUN useradd -mU -G sudo -s /bin/bash gst
#RUN echo "gst\ngst"|passwd gst
#RUN echo 'root:root' | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd
RUN mkdir /var/run/sshd

EXPOSE 22
#CMD ["/usr/sbin/sshd", "-D"]

# For example:
#docker run --privileged -d -P --name gstreamer $(gstreamer_images)
#docker port gstreamer 22
