FROM ubuntu

RUN apt-get update && apt-get install -y \
    --no-install-recommends \
    python-pip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN pip install setuptools && pip install shadowsocks

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

