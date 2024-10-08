FROM rockylinux:9

RUN yum install -y python3 
RUN yum install -y openssh-server
RUN python3 -m ensurepip
RUN python3 -m pip install --no-cache-dir -U ansible
RUN yum install -y initscripts
RUN ssh-keygen -A
RUN yum install -y centos-release-gluster9
RUN yum install -y glusterfs-server
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

EXPOSE 22

ENTRYPOINT  /bin/bash -c "/usr/sbin/sshd -D && sleep 10000"