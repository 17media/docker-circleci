FROM        alpine:3.6

RUN         apk --no-cache add --virtual .rundeps \
                build-base \
                git \
                openssh-client \
                parallel \
                curl \
                ca-certificates \
                tar \ 
                gzip \
                coreutils \
                jq && \
            apk --no-cache add -X http://dl-cdn.alpinelinux.org/alpine/edge/community --virtual .rundeps \
                docker

            # Add gcloud
RUN         apk --no-cache add --virtual .gcloud-builddeps \
                tar && \
            apk --no-cache add --virtual .gcloud-rundeps \
                python2 python3 && \
            mkdir -p /usr/src/google-cloud-sdk && \
            curl -sSL https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz | tar xz -C /usr/src/google-cloud-sdk --strip-components 1 && \
            ( \
                cd /usr/src/google-cloud-sdk && \
                ./install.sh --usage-reporting false --path-update true \
            ) && \
            ln -s /usr/src/google-cloud-sdk/bin/* /usr/local/bin/. && \
            apk del .gcloud-builddeps
