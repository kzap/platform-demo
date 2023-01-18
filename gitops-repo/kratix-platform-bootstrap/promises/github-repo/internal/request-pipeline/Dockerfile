FROM "alpine"

LABEL org.opencontainers.image.authors "andre@ada.support"
LABEL org.opencontainers.image.source https://github.com/kzap/platform-demo

RUN [ "mkdir", "/tmp/transfer" ]
RUN apk update && apk add --no-cache yq git github-cli curl

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.25.1/bin/linux/amd64/kubectl
RUN chmod u+x kubectl && mv kubectl /bin/kubectl

ADD resources/* /tmp/transfer/
ADD execute-pipeline execute-pipeline

CMD [ "sh", "-c", "./execute-pipeline" ]
ENTRYPOINT []
