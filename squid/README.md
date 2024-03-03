# Squid integration notes

Clone the repo and adjust `config.yaml` for your environment.


## General Notes

- You'll need `squid-openssl` in Debian.
- An example ICAP server is provided in [Clotho](https://github.com/ClothoProxy/Clotho/src/bin/squid-icap.rs).
- This has been tested using Squid v5.7

The example ICAP config provided _should_ work out of the box. The `sts` endpoints are allowlisted to allow for `AssumeRole*`.
You can achieve the same with Clotho by allowing `sts` in all accounts and all regions.


