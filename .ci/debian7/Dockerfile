FROM debian:7

RUN apt-get update \
    && apt-get install -y wget git zip  build-essential debhelper libncurses5-dev unixodbc unixodbc-dev openjdk-7-jdk libssl-dev curl unzip
RUN wget http://erlang.org/download/otp_src_21.2.tar.gz &&  tar zxvf otp_src_21.2.tar.gz && cd otp_src_21.2 && ./configure && make && make install
RUN mkdir -p /root/.ssh/
# cleanup
RUN apt-get clean\
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /otp_src_21.2/* /otp_src_21.2.tar.gz

ADD ./files/id_rsa /root/.ssh/
ADD ./files/id_rsa.pub /root/.ssh/
ADD ./files/config /root/.ssh/
ADD ./files/emqx_ci.sh /
ADD ./files/emqx_install_test.sh /

RUN chmod +x /emqx_ci.sh /emqx_install_test.sh

CMD ["/bin/bash", "-c", "source /emqx_ci.sh"]
