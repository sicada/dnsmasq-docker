FROM alpine:edge
LABEL maintainer="nviera@sicada.com"

# webproc release settings
ENV WEBPROC_VERSION 0.2.2
ENV WEBPROC_URL https://github.com/jpillora/webproc/releases/download/$WEBPROC_VERSION/webproc_linux_amd64.gz

# fetch dnsmasq and webproc binary
RUN apk update \
 && apk --no-cache add dnsmasq nano 
 
RUN apk add --no-cache --virtual .build-deps curl
 && curl -sL $WEBPROC_URL | gzip -d - > /usr/local/bin/webproc \
 && chmod +x /usr/local/bin/webproc \
 && apk del .build-deps

#configure dnsmasq
RUN mkdir -p /etc/default/
RUN mkdir -p /etc/dnsmasq.d/
RUN mkdir -p /var/lib/misc/

RUN touch /var/lib/misc/dnsmasq.leases
RUN echo -e "ENABLED=1\nIGNORE_RESOLVCONF=yes" > /etc/default/dnsmasq
COPY dnsmasq.conf /etc/dnsmasq.conf

EXPOSE 53/tcp
EXPOSE 53/udp
EXPOSE 67/udp
EXPOSE 68/udp
EXPOSE 8080/tcp

#run!
ENTRYPOINT ["webproc","--config","/etc/dnsmasq.conf","--","dnsmasq","--no-daemon", "--dhcp-broadcast"]
