# Note
## How to build and push?
```
docker buildx build \
--build-arg 'http_proxy=http://clash.internal.moqi.ai:7890' \
--build-arg 'https_proxy=http://clash.internal.moqi.ai:7890' \
--build-arg 'no_proxy=localhost,127.0.0.0/8,10.0.0.0/8,172.16.0.0/12,192.168.0.0/16,docker,git.moqi.ai,.internal.moqi.ai' \
--platform linux/amd64 \
--build-arg version="latest" \
--rm=true \
-t mochix/ubuntu22.04_base:0.0.1 . --push
```

harbor.internal.moqi.ai/mochix/ubuntu22.04_base:0.0.1

## How to build x86 and arm?
```
docker buildx build \
--build-arg 'http_proxy=http://clash.internal.moqi.ai:7890' \
--build-arg 'https_proxy=http://clash.internal.moqi.ai:7890' \
--build-arg 'no_proxy=localhost,127.0.0.0/8,10.0.0.0/8,172.16.0.0/12,192.168.0.0/16,docker,git.moqi.ai,.internal.moqi.ai' \
--platform linux/arm64,linux/amd64 \
--build-arg version="latest" \
--rm=true \
-t mochix/jammy . \
--push
```