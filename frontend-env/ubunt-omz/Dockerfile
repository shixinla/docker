FROM ubuntu
LABEL author="shixinla shixin.work@outlook.com"


# 用 root 用户操作
USER root

# 设置时区
ARG TZ=Asia/Shanghai
ENV TZ ${TZ}

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 更换阿里云源
RUN sed -i "s/security.ubuntu.com/mirrors.aliyun.com/" /etc/apt/sources.list; \
    sed -i "s/archive.ubuntu.com/mirrors.aliyun.com/" /etc/apt/sources.list; \
    sed -i "s/security-cdn.ubuntu.com/mirrors.aliyun.com/" /etc/apt/sources.list

RUN apt-get clean

# 更新源，安装相应工具
RUN apt-get update; \
    apt-get install -y \
    zsh \
    vim \
    wget \
    curl \
    git-core

# 安装omz(使用GitHub镜像地址加速下载)
RUN git clone https://github.com.cnpmjs.org/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh; \
    cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc; \
    git clone https://github.com.cnpmjs.org/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions; \
    git clone https://github.com.cnpmjs.org/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting; \
    sed -i 's/^plugins=(/plugins=(zsh-autosuggestions zsh-syntax-highlighting z /' ~/.zshrc; \
    chsh -s /usr/bin/zsh

# 删除 apt/lists
RUN rm -rf /var/lib/apt/lists/*