FROM python:3.4-alpine

MAINTAINER kwens <pkkewenshu@outlook.com>

# COPY BY zeromake/base-uwsgi thanks zeromake's help. here is his github https://github.com/zeromake

# 更换到阿里云
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# 设置时区语言
ENV TZ Asia/Shanghai
ENV PYTHONIOENCODING utf8

COPY requirements.txt /tmp/requirements.txt

# 设置默认pip镜像
RUN mkdir -p ~/.pip && echo -e "[global]\ntimeout = 6000\nindex-url = https://pypi.doubanio.com/simple\n\n[install]\nuse-mirrors = true\nmirrors = https://pypi.doubanio.com/simple\ntrusted-host = pypi.doubanio.com" > ~/.pip/pip.conf

# 安装python包的依赖
RUN apk add --no-cache --virtual .build-deps mariadb-dev linux-headers postgresql-dev && \
    pip install uwsgi --no-cache-dir && \
    pip install numpy --no-cache-dir && \
    pip install  -r /tmp/requirements.txt --no-cache-dir
RUN apk add --no-cache mariadb-client-libs libpq tzdata

RUN rm -rf /tmp/requirements.txt

# RUN sed -i 's/>= 80300/>= 80301/g' /usr/lib/python2.7/site-packages/psycopg2/extras.py