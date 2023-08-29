# reference: https://hub.docker.com/r/phusion/baseimage/tags
FROM phusion/baseimage:jammy-1.0.1

ENV HOME /root

# 修改源
ARG apt_archive="https://mirrors.tuna.tsinghua.edu.cn"
RUN sed -i "s|http://archive.ubuntu.com|$apt_archive|g" /etc/apt/sources.list

RUN apt-get update --allow-releaseinfo-change
RUN apt-get install --yes ca-certificates bash python3 tar wget git python3-pip curl python3-pika tmux zsh libomp-dev
RUN python3 -m pip install -U typer h5py tqdm elasticsearch pymilvus qdrant-client redis weaviate-cli pinecone-client myscaledb-client clickhouse-connect clickhouse-driver nest_asyncio cos-python-sdk-v5 -i https://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com

# ohmyzsh
RUN sh -c "$(wget https://mochi-cloud.oss-cn-qingdao.aliyuncs.com/install.sh -O -)"

# 生成SSH keys,baseimage-docker不包含任何的key,所以需要你自己生成.你也可以注释掉这句命令,系统在启动过程中,会生成一个.
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# 初始化baseimage-docker系统
CMD ["/sbin/my_init"]

# 这里可以放置你自己需要构建的命令

# 当完成后,清除APT.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*