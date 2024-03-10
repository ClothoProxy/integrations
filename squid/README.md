# Squid integration notes

Clone the repo and adjust `config.yaml` for your environment.


## How to

Server:


```sh
git clone https://github.com/ClothoProxy/integrations
cd integrations/squid
git clone https://github.com/ClothoProxy/Clotho
docker build -t clothoproxy .
docker run  -p 3128:3128 -v $(pwd)/config.yaml:/usr/sbin/config.yaml  -it clothoproxy
```

`config.yaml` is your allowlist.


Client:

```sh 
export http_proxy=http://SERVER_IP:3128
export https_proxy=http://SERVER_IP:3128
aws s3 ls --no-verify-ssl
```


## General Notes

- You'll need `squid-openssl` in Debian.
- An example ICAP server is provided in [Clotho](https://github.com/ClothoProxy/Clotho/src/bin/squid-icap.rs).
- This has been tested using Squid v5.7

The example ICAP config provided _should_ work out of the box. The `sts` endpoints are allowlisted to allow for `AssumeRole*`.
You can achieve the same with Clotho by allowing `sts` in all accounts and all regions.


