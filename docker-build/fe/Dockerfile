# 选择基础镜像
FROM openjdk:8u342-jdk

# 设置环境变量
ENV JAVA_HOME="/usr/local/openjdk-8/" \
    PATH="/opt/apache-doris/fe/bin:$PATH"

# 下载软件至镜像内，可根据需要替换
COPY ./resource/fe-2.0.4.tar.gz /opt/

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
    mkdir -p /opt/apache-doris/fe && \
    cd /opt && \
    tar -xvf /opt/fe-2.0.4.tar.gz -C /opt/apache-doris/fe

COPY ./resource/init_fe.sh /opt/apache-doris/fe/bin
RUN chmod 755 /opt/apache-doris/fe/bin/*.sh

ENTRYPOINT ["/opt/apache-doris/fe/bin/init_fe.sh"]
