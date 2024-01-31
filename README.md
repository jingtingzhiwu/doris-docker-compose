# doris-docker-compose
基于最新的doris二进制包https://doris.apache.org/zh-CN/download <br>

解压后需自行拆分打包fe.tar.gz、be.tar.gz、broker.tar.gz<br>

目录结构如下<br>
[root@localhost docker-build]# tree -L 3 ./<br>
./<br>
├── be<br>
│   ├── Dockerfile<br>
│   └── resource<br>
│       ├── be-2.0.4.tar.gz<br>
│       └── init_be.sh<br>
├── broker<br>
│   ├── Dockerfile<br>
│   └── resource<br>
│       ├── broker-2.0.4.tar.gz<br>
│       └── init_broker.sh<br>
└── fe<br>
    ├── Dockerfile<br>
    └── resource<br>
        ├── fe-2.0.4.tar.gz<br>
        └── init_fe.sh<br>

<code>docker run -itd \
--name=fe \
--env FE_SERVERS="fe1:192.168.4.170:9010" \
--env FE_ID=1 \
-p 8030:8030 \
-p 9030:9030 \
-v /data/fe/doris-meta:/opt/apache-doris/fe/doris-meta \
-v /data/fe/log:/opt/apache-doris/fe/log \
--net=host --privileged=true \
wilkey:doris-2.0.4-fe
</code>

<code>docker run -itd \
--name=be \
--env FE_SERVERS="fe1:192.168.4.170:9010" \
--env BE_ADDR="192.168.4.170:9050" \
-p 8040:8040 \
-v /data/be/storage:/opt/apache-doris/be/storage \
-v /data/be/log:/opt/apache-doris/be/log \
--net=host --privileged=true \
wilkey:doris-2.0.4-be
</code>
