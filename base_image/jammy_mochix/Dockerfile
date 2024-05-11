# reference: https://hub.docker.com/r/phusion/baseimage/tags
FROM phusion/baseimage:jammy-1.0.1

ENV HOME /root

# change source
ARG apt_archive="https://mirrors.tuna.tsinghua.edu.cn"
RUN sed -i "s|http://archive.ubuntu.com|$apt_archive|g" /etc/apt/sources.list

RUN apt-get update --allow-releaseinfo-change
RUN apt-get install --yes ca-certificates bash python3 tar wget git python3-pip curl python3-pika tmux zsh libomp-dev cmake clang-15 libssl-dev
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
RUN apt-get install --yes openssh-server ninja-build rsync llvm 
# Update PATH to include the Rust toolchain
ENV PATH="/root/.cargo/bin:${PATH}"
RUN rustup toolchain install nightly-2023-12-02 --profile minimal --component llvm-tools-preview
# RUN rustup default nightly-2023-09-10
RUN cargo install cargo-llvm-cov grcov


RUN python3 -m pip install lcov-cobertura
RUN apt-get install --yes file bc
RUN python3 -m pip install coscmd -U

# ohmyzsh
RUN sh -c "$(wget https://mochi-cloud.oss-cn-qingdao.aliyuncs.com/install.sh -O -)"

# Generate SSH keys,baseimage-docker will not include any keys
# You can delete this command, cause keys will be generated when system start.
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

# Init baseimage-docker system
CMD ["/sbin/my_init"]

RUN echo '[common]' > /root/.cos.conf && \
    echo 'secret_id = SED_SECRET_ID_SED' >> /root/.cos.conf && \
    echo 'secret_key = SED_SECRET_KEY_SED' >> /root/.cos.conf && \
    echo 'bucket = SED_BUCKET_SED' >> /root/.cos.conf && \
    echo 'region = SED_REGION_SED' >> /root/.cos.conf && \
    echo 'max_thread = 5' >> /root/.cos.conf && \
    echo 'part_size = 1' >> /root/.cos.conf && \
    echo 'retry = 10' >> /root/.cos.conf && \
    echo 'timeout = 60' >> /root/.cos.conf && \
    echo 'schema = https' >> /root/.cos.conf && \
    echo 'verify = md5' >> /root/.cos.conf && \
    echo 'anonymous = False' >> /root/.cos.conf && \
    echo '' >> /root/.cos.conf

# Put your DIY command here.
# 设置工作目录
WORKDIR /root

# 运行容器时的默认命令
# CMD ["tail", "-f", "/dev/null"]
# Clean APT
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*