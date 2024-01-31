# 选择基础镜像
FROM openjdk:8u342-jdk

# 设置环境变量
ENV JAVA_HOME="/usr/local/openjdk-8/" \
    PATH="/opt/apache-doris/be/bin:$PATH"

# 下载软件至镜像内，可根据需要替换
COPY ./resource/be-2.0.4.tar.gz /opt/

RUN sed -i "1ideb https://mirrors.aliyun.com/debian/ bullseye main non-free contrib" /etc/apt/sources.list
RUN sed -i "2ideb-src https://mirrors.aliyun.com/debian/ bullseye main non-free contrib" /etc/apt/sources.list
RUN sed -i "3ideb https://mirrors.aliyun.com/debian-security/ bullseye-security main" /etc/apt/sources.list
RUN sed -i "4ideb-src https://mirrors.aliyun.com/debian-security/ bullseye-security main" /etc/apt/sources.list
RUN sed -i "5ideb https://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib" /etc/apt/sources.list
RUN sed -i "6ideb-src https://mirrors.aliyun.com/debian/ bullseye-updates main non-free contrib" /etc/apt/sources.list
RUN sed -i "7ideb https://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib" /etc/apt/sources.list
RUN sed -i "8ideb-src https://mirrors.aliyun.com/debian/ bullseye-backports main non-free contrib" /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y default-mysql-client && \
    apt-get clean && \
    mkdir -p /opt/apache-doris/be && \
    cd /opt && \
    tar -xvf /opt/be-2.0.4.tar.gz -C /opt/apache-doris/be

COPY ./resource/init_be.sh /opt/apache-doris/be/bin
RUN chmod 755 /opt/apache-doris/be/bin/*.sh

ENTRYPOINT ["/opt/apache-doris/be/bin/init_be.sh"]
