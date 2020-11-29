FROM centos:7

#install ssh server 
RUN yum -y install openssh-server

#create user and giving passwd and create .ssh dir with owner permission
RUN useradd remote_user &&  \
    echo "root" | passwd remote_user --stdin && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh

#copy public key geneerated to contianer ssh authenticated ssh con.
#Copy from machine to cotainer
COPY root-key.pub /home/remote_user/.ssh/authorized_keys

#change owner and set permissions towrite and execute -- no read!!
RUN chown remote_user:remote_user -R /home/remote_user/.ssh/ && \ 
    chmod 600 /home/remote_user/.ssh/authorized_keys

#generating some keys for ssh
RUN /usr/sbin/sshd-keygen

#start service
CMD /usr/sbin/sshd -D
