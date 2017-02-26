FROM ubuntu:17.04
MAINTAINER 牟勇 <my24251325@gmail.com>

RUN sed -i 's/archive.ubuntu/mirrors.aliyun/' /etc/apt/sources.list

RUN apt-get update && apt-get install -y --no-install-recommends python-pip && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clien

RUN pip install setuptools 
RUN pip install shadowsocks

ARG PASSWORD=password
ARG PORT=8388

EXPOSE ${PORT}

RUN echo "{ \
    \"server\":\"0.0.0.0\", \
    \"port_password\": { \
        \"${PORT}\": \"${PASSWORD}\" \
    }, \
    \"timeout\":300, \
    \"method\":\"aes-256-cfb\", \
    \"fast_open\": false \
}" > /ss.json

CMD ["ssserver", "-c", "/ss.json"]
