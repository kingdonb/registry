FROM registry:2.6.0

RUN apk add --no-cache \
        python3 && \
    python3 -m ensurepip && \
    ln -sf /usr/bin/python3 /usr/bin/python && \
    ln -sf /usr/bin/pip3 /usr/bin/pip

RUN buildDeps='gcc git linux-headers musl-dev python3-dev libffi-dev openssl-dev' && \
    apk add --no-cache $buildDeps && \
    # "upgrade" boto to 2.43.0 + the patch to fix minio connections
    pip install --disable-pip-version-check --no-cache-dir --upgrade \
        git+https://github.com/teamhephy/boto@abb38474ee5124bb571da0c42be67cd27c47094f \
        azure==4.0.0 \
        azure-storage-blob==12.2.0 \
        google-cloud==0.34.0 \
        oauth2client==4.1.3 \
        google-api-python-client==1.7.11 \
        python-swiftclient==3.9.0 \
        python-keystoneclient==3.22.0 && \
    # purge dev dependencies
    apk del $buildDeps

COPY . /

VOLUME ["/var/lib/registry"]
CMD ["/opt/registry/sbin/registry"]
EXPOSE 5000
