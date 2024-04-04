FROM rust:slim-bookworm as builder

WORKDIR /Clotho
COPY Clotho/ /Clotho
RUN cargo build --bin clothohud --release

FROM debian:bookworm-slim
RUN apt-get update && apt-get install -y  supervisor && apt-get clean

RUN mkdir -p /etc/clotho/ && mkdir -p /etc/ssl/localcerts
RUN openssl genrsa 2048 > /etc/ssl/localcerts/clothohud.key
RUN openssl req -new -x509 -nodes -days 365000 -subj "/C=GB/O=Clotho Proxy/CN=amazonaws.com" -key /etc/ssl/localcerts/clothohud.key -out /etc/ssl/localcerts/clothohud.cer

COPY config.yaml /etc/clotho/config.yaml
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf


COPY --from=builder /Clotho/target/release/clothohud /usr/sbin/clothohud
RUN chmod +x /usr/sbin/clothohud


EXPOSE 8000 8000
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
