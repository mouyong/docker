FROM ubuntu:17.04
MAINTAINER 牟勇 <my24251325@gmail.com>

RUN sed -i 's/archive.ubuntu/mirrors.aliyun/' /etc/apt/sources.list

RUN apt-get update && apt-get install -y --no-install-recommends python-pip && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clien

RUN pip install setuptools 
RUN pip install shadowsocks

ARG SERVER=0.0.0.0
ARG PASSWORD=password
ARG PORT=8388

EXPOSE ${PORT}

RUN echo "{ \
    \"server\":\"${SERVER}\", \
    \"port_password\": { \
        \"${PORT}\": \"${PASSWORD}\" \
    }, \
    \"timeout\":300, \
    \"method\":\"aes-256-cfb\", \
    \"fast_open\": false \
}" > /ss.json

ENTRYPOINT ["ssserver", "-c", "/ss.json"]

CMD ["bash"]
