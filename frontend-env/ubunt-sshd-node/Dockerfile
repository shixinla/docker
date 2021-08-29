FROM shixinla/ubunt-sshd
LABEL author="shixinla shixin.work@outlook.com"

# 用 root 用户操作
USER root

RUN apt-get clean

# node相关环境变量
ENV NVM_DIR=/root/.nvm
ENV NODE_VERSION=v16

# 配置git用户
RUN git config --global user.name "shixinla"
RUN git config --global user.emai "shixin.work@outlook.com"

# 安装nvm与node
RUN git clone https://github.com.cnpmjs.org/nvm-sh/nvm.git ${NVM_DIR}; \
    cd ${NVM_DIR} && git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)` && . ${NVM_DIR}/nvm.sh; \
    nvm install ${NODE_VERSION}; \
    nvm use ${NODE_VERSION}; \
    nvm alias ${NODE_VERSION}; \
    npm i -g nrm; \
    nrm use taobao; \
    npm i -g yarn; \
    npm i -g commitizen

RUN echo '' >> ~/.zshrc; \
    echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc; \
    echo '[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm' >> ~/.zshrc; 

EXPOSE 21
EXPOSE 80
EXPOSE 8080
EXPOSE 8888
EXPOSE 3333

WORKDIR /workspace