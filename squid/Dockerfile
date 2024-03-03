FROM rust:slim-bookworm as builder

WORKDIR /Clotho
COPY Clotho/ /Clotho
RUN cargo build --bin squid-icap --release

FROM debian:bookworm-slim
RUN apt-get update && apt-get install -y squid-openssl supervisor && apt-get clean

RUN openssl genrsa 2048 > /etc/squid/ca_key.pem
RUN openssl req -new -x509 -nodes -days 365000 -subj "/C=GB/O=Clotho Proxy/CN=example.com" -key /etc/squid/ca_key.pem -out /etc/squid/ca_cert.pem

RUN mkdir -p /var/lib/squid
RUN /usr/lib/squid/security_file_certgen -c -s /var/lib/squid/ssl_d -M 12MB

COPY config.yaml /usr/sbin/config.yaml
COPY squid.conf /etc/squid/squid.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf


COPY --from=builder /Clotho/target/release/squid-icap /usr/sbin/icapd
RUN chmod +x /usr/sbin/icapd


EXPOSE 3128 3128
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
