FROM rockylinux:9

RUN yum install -y python3 
RUN yum install -y openssh-server openssh-clients
RUN python3 -m ensurepip
RUN python3 -m pip install --no-cache-dir -U ansible
RUN ansible-galaxy collection install gluster.gluster
RUN ansible-galaxy collection install ansible.posix
RUN yum install -y initscripts
RUN ssh-keygen -A
RUN echo 'root:pass' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN echo "Host *" >> ~/.ssh/config
RUN echo "  StrictHostKeyChecking no" >> ~/.ssh/config
RUN yum install -y sshpass

EXPOSE 22

ENTRYPOINT  /bin/bash -c "/usr/sbin/sshd -D && sleep 10000"