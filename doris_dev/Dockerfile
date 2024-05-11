FROM apache/doris:build-env-ldb-toolchain-latest
# 设置环境变量（基于 apache/doris:build-env-ldb-toolchain-latest `docker inspect` 的输出）
# ENV PATH=/var/local/ldb-toolchain/bin/:/var/local/thirdparty/installed/bin/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
#     JAVA_HOME=/usr/lib/jvm/java-1.8.0 \
#     MAVEN_HOME=/usr/share/maven \
#     REPOSITORY_URL=https://doris-thirdparty-repo.bj.bcebos.com/thirdparty \
#     DEFAULT_DIR=/var/local \
#     DORIS_THIRDPARTY=/var/local/thirdparty


# 添加 mochix 用户。请确保 UID 和 GID 与宿主机上的 mochix 用户相匹配。
# 您可以通过在宿主机上运行 `id mochix` 来获取 UID 和 GID。
# 以下的 1000:1000 只是一个例子，您可能需要根据实际情况进行修改。
# RUN groupadd -g 1000 mochix && useradd -u 1000 -g 1000 -m mochix
RUN yum install -y sudo \
        && useradd -ms /bin/bash mochix && echo 294207 | passwd mochix --stdin \
        && usermod -a -G wheel mochix

USER root
# # 设置 zsh
RUN yum install -y zsh
# RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh \
#         && git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions \
#         && git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting


USER mochix
# 设置工作目录
WORKDIR /home/mochix

# 运行容器时的默认命令
CMD ["tail", "-f", "/dev/null"]
