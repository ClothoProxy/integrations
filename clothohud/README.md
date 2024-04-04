# Clothohud integration notes

Clone the repo and adjust `config.yaml` for your environment.


## How to

Server:


```sh
git clone https://github.com/ClothoProxy/integrations
cd integrations/clothohud
git clone https://github.com/ClothoProxy/Clotho
docker build -t clothohud .
docker run  -p 8000:8000-it clothohud
```

`config.yaml` is your allowlist.


Client:

```sh 
export http_proxy=http://SERVER_IP:8000
export https_proxy=http://SERVER_IP:8000
aws s3 ls --no-verify-ssl
```


## General Notes

You _might_ need to add STS endpoints to your allowlist
