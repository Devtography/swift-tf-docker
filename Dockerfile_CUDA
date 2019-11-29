# Customised Swift for TensorFlow image with Python installed.
FROM swift:5.1-bionic AS toolchain

FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04

LABEL \
    maintainer="Wing Chau <wing@devtography.com>" \
    version="1.0" \
    description="An Ubuntu 18.04 Docker image for Swift for TensorFlow." \
    ubuntu-version="18.04" \
    swift-tensorflow-version="v0.5.0" \
    python-version="3.6.x" \
    cuda-version="10.0" \
    license="Apache License 2.0"

ENV DEBIAN_FRONTEND=noninteractive

WORKDIR /root/

RUN apt update \
    && apt-mark hold cuda-compat-10-0 libcudnn7 libcudnn7-dev \
    libnccl-dev libnccl2 \
    && apt upgrade -y \
    && apt clean

# Install & setup Swift for TensorFlow toolchain.
RUN apt install -y curl pv \
    # Install Swift dependencies.
    && apt install -y --no-install-recommends git cmake ninja-build clang \
    uuid-dev libicu-dev icu-devtools libedit-dev libxml2-dev libsqlite3-dev \
    swig libpython3-dev libncurses5-dev pkg-config libcurl4-openssl-dev \
    systemtap-sdt-dev tzdata rsync \
    && apt install -y --no-install-recommends libblocksruntime-dev \
    && curl -L https://storage.googleapis.com/swift-tensorflow-artifacts/releases/v0.5/rc1/swift-tensorflow-RELEASE-0.5-cuda10.0-cudnn7-ubuntu18.04.tar.gz \
    -o ./swift-tensorflow.tar.gz \
    && pv swift-tensorflow.tar.gz | tar xzf - -C . \
    && rm swift-tensorflow.tar.gz  \
    && apt remove -y curl pv \
    && apt autoremove -y \
    && apt clean

COPY --from=toolchain /usr/bin/sourcekit-lsp usr/bin/sourcekit-lsp

ENV PATH "/root/usr/bin:${PATH}"

# Install Python3.6
RUN apt install -y python3.6 \
    && apt install -y --no-install-recommends python3-pip \
    && apt clean \
    && ln -sf python3.6 /usr/bin/python \
    && ln -sf pip3 /usr/bin/pip \
    && pip install --upgrade pip

CMD ["bash"]
