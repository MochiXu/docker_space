# 说明
## 执行流程
```
docker buildx build --build-arg 'http_proxy=http://clash.internal.moqi.ai:7890' --build-arg 'https_proxy=http://clash.internal.moqi.ai:7890' --build-arg 'no_proxy=localhost,127.0.0.0/8,10.0.0.0/8,172.16.0.0/12,192.168.0.0/16,docker,git.moqi.ai,.internal.moqi.ai' --platform linux/amd64 --build-arg version="latest" --rm=true -t mochix/ubuntu22.04_base . --push
```