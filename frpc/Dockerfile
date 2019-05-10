FROM alpine:latest

LABEL maintainer="Memet Eli Nizam <almas1992@126.com>"

WORKDIR /etc/frpc


ARG CHANGE_SOURCE=true
RUN if [ ${CHANGE_SOURCE} = true ]; then \
    sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories \
;fi

RUN apk --update add --no-cache --virtual .build-deps \
       curl && \
       curl -s https://api.github.com/repos/fatedier/frp/releases/latest | \
       grep browser_download_url | \
       grep linux_amd64 | \
       cut -d '"' -f 4 | \
       xargs curl -L | \
       tar -zx -C . --strip-components=1 && \
       mv frpc /usr/local/bin/frpc && \ 
       rm -fr ./* && \
       apk del .build-deps && \
       rm -rf /var/cache/apk/*

CMD ["frpc"]
