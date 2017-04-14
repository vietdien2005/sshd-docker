FROM centos:7

MAINTAINER Dam Viet <vietdien2005@gmail.com>

RUN yum update -y
RUN yum install -y passwd openssh openssh-server openssh-clients initscripts sudo

RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
	sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

RUN sed -ri 's/account    required     pam_nologin.so/#account    required     pam_nologin.so/' /etc/pam.d/login && \
	sed -ri 's/account    required     pam_nologin.so/#account    required     pam_nologin.so/' /etc/pam.d/sshd

RUN mkdir /root/.ssh && \
	touch /root/.ssh/authorized_keys && \
	echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDUVTKXeZLsx3ClXQAgu0gE30Pmh/v2cvZN9XzP+GnVfmupRn+J0ithW99cZ3es2auUYSunexAjfIORyVKEKasEhvymYQ4ywfQzo069P6jhbXarEttfhkDiVSBus+L3+VmTbBCtLfa6gMF3ay2TmGDFELLK8VBHSmIkyYJBnkTiw742LbOttDDYBpV1bUTmJgOK5DFTVgTFxiKr/qMosaphrV8prk5wxL7JxGBWoIDbZpxe6Y+R95p4HGjsH26c71BwgS++CJ8TiTtcOak/0e8xAll1SF4bMxbzrrHoywoANZcuGes4sCHGqVoRgWbg2Kt4HncyM34cuBPh+gwxNdoV" >> /root/.ssh/authorized_keys && \
	chmod 600 /root/.ssh/authorized_keys && \
	chmod 700 /root/.ssh 

RUN /usr/sbin/sshd-keygen

CMD ["/usr/sbin/sshd", "-D"]