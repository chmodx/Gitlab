FROM alpine:latest

RUN adduser -D -S -h /home/gitlab-runner gitlab-runner

RUN apk --update add \
  bash \
  shadow \
  dcron \
  iproute2 \ 
  iptables \
  ca-certificates \
  openssh-client  \
  git \
  curl \
  e2fsprogs \
  openrc \
  docker \
  make \
  rsyslog \
  tzdata \
  py-pip \
  xz

RUN curl -s -o /usr/bin/gitlab-ci-multi-runner https://gitlab-ci-multi-runner-downloads.s3.amazonaws.com/latest/binaries/gitlab-ci-multi-runner-linux-amd64
RUN pip install docker-compose

RUN usermod -aG docker gitlab-runner

RUN chmod +x /usr/bin/gitlab-ci-multi-runner
RUN ln -s /usr/bin/gitlab-ci-multi-runner /usr/bin/gitlab-runner

RUN gitlab-runner --version
RUN docker --version
RUN docker-compose --version

RUN rm -rf /var/cache/apk/*
RUN touch /var/log/lastlog

RUN mkdir /lib64 && \
    ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

COPY ./service/timezone /etc/init.d/timezone
COPY ./service/gitlab-runner /etc/init.d/gitlab-runner

RUN chmod +x /etc/init.d/timezone
RUN chmod +x /etc/init.d/gitlab-runner    

RUN sed -i '/tty/d' /etc/inittab && \
                sed -i 's/#rc_sys=""/rc_sys="docker"/g' /etc/rc.conf && \
                echo 'rc_provide="loopback net"' >> /etc/rc.conf && \
                sed -i 's/^#\(rc_logger="YES"\)$/\1/' /etc/rc.conf && \
                sed -i 's/hostname $opts/# hostname $opts/g' /etc/init.d/hostname && \
                sed -i 's/mount -t tmpfs/# mount -t tmpfs/g' /lib/rc/sh/init.sh && \
                sed -i 's/cgroup_add_service /# cgroup_add_service /g' /lib/rc/sh/openrc-run.sh
                

RUN rm -f /etc/init.d/hwclock \
        /etc/init.d/hwdrivers \
        /etc/init.d/modules \
        /etc/init.d/modules-load \
        /etc/init.d/modloop    

RUN rc-update add docker default && \
    rc-update add timezone default && \
    rc-update add gitlab-runner default && \
    rc-update add rsyslog default && \
    rc-update add dcron default

VOLUME ["/var/lib/docker", "/etc/gitlab-runner", "/home/gitlab-runner"]
ENTRYPOINT ["/sbin/init"]

