FROM ubuntu:18.04

RUN apt-get update \ 
    && apt-get install -y wget git zip curl unzip
RUN apt-get update \ 
    && apt-get install -y build-essential debhelper
RUN wget http://packages.erlang-solutions.com/site/esl/esl-erlang/FLAVOUR_1_general/esl-erlang_21.2-1~ubuntu~bionic_amd64.deb -O /tmp/erlang.deb
RUN dpkg -i /tmp/erlang.deb || true
RUN apt-get -f install -y
RUN mkdir -p /root/.ssh/
# cleanup
RUN apt-get clean\
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD ./files/id_rsa /root/.ssh/
ADD ./files/id_rsa.pub /root/.ssh/
ADD ./files/config /root/.ssh/
ADD ./files/emqx_ci.sh /
ADD ./files/emqx_install_test.sh /

RUN chmod +x /emqx_ci.sh /emqx_install_test.sh

CMD ["/bin/bash", "-c", "source /emqx_ci.sh"]