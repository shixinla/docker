FROM shixinla/ubunt-omz
LABEL author="shixinla shixin.work@outlook.com"

# 用 root 用户操作
USER root

RUN apt-get clean

# 更新源，安装相应工具
RUN apt-get update; \
    apt-get install -y \
    openssh-client \
    openssh-server

# 允许root ssh登录
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
RUN mkdir -p /run/sshd

# 修改root用户密码，用于远程ssh 登录
RUN ssh-keygen -A
RUN echo 'root:shixinla' | chpasswd


# 删除 apt/lists
RUN rm -rf /var/lib/apt/lists/*

EXPOSE 22

CMD [ "/usr/sbin/sshd", "-D", "-f", "/etc/ssh/sshd_config" ]
