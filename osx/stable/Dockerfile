FROM rust:1.43.1

RUN apt update
RUN apt install -y clang gcc g++ cmake zlib1g-dev libmpc-dev libmpfr-dev libgmp-dev

RUN rustup target add x86_64-apple-darwin

RUN git clone https://github.com/tpoechtrager/osxcross
WORKDIR /osxcross
RUN wget -nc https://s3.dockerproject.org/darwin/v2/MacOSX10.10.sdk.tar.xz
RUN mv MacOSX10.10.sdk.tar.xz tarballs/
RUN UNATTENDED=yes OSX_VERSION_MIN=10.7 ./build.sh

WORKDIR /osxcross/target/bin
RUN bash -c 'for file in ./*; do ln -s file /bin/$file; done'
WORKDIR /

CMD ["/bin/bash"]
