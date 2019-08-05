FROM python:3-alpine3.6

MAINTAINER kwens <pkkewenshu@outlook.com>

# COPY BY zeromake/base-uwsgi. here is his github https://github.com/zeromake

# 更换到阿里云
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories

# 设置时区语言
RUN apk add --no-cache tzdata ca-certificates
ENV TZ Asia/Shanghai

RUN pip install --upgrade pip

RUN pip install --upgrade setuptools

# 安装依赖
RUN apk update && apk add \
        libuuid \
        pcre \
        mailcap \
        gcc \
	g++ \
        libc-dev \
	libffi-dev \
        linux-headers \
        pcre-dev \
		jpeg-dev \
		mariadb-dev \
		postgresql-dev \
		python-dev \
    && pip install --no-cache-dir uWSGI>=2.0.15 \
    && rm -rf /tmp/*

# 安装NGINX
RUN apk add nginx --no-cache

# 设置默认pip镜像
RUN mkdir -p ~/.pip && echo -e "[global]\ntimeout = 6000\nindex-url = https://pypi.doubanio.com/simple\n\n[install]\nuse-mirrors = true\nmirrors = https://pypi.doubanio.com/simple\ntrusted-host = pypi.doubanio.com" > ~/.pip/pip.conf
