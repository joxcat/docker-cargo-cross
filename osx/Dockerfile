FROM debian:stretch as osxcross
RUN apt update
RUN apt install -y git wget clang gcc g++ cmake zlib1g-dev libssl-dev libmpc-dev libmpfr-dev libgmp-dev libxml2-dev
RUN git clone https://github.com/tpoechtrager/osxcross
WORKDIR /osxcross
RUN wget -nc https://s3.dockerproject.org/darwin/v2/MacOSX10.10.sdk.tar.xz
RUN mv MacOSX10.10.sdk.tar.xz tarballs/
RUN UNATTENDED=yes OSX_VERSION_MIN=10.7 ./build.sh

FROM rust:latest as stable
RUN apt update
RUN apt install -y clang
RUN rustup target add x86_64-apple-darwin
COPY --from=osxcross /osxcross /osxcross
WORKDIR /osxcross/target/bin
RUN bash -c 'for file in ./*; do ln -s file /bin/$file; done'
WORKDIR /
CMD ["/bin/bash"]

FROM instrumentisto/rust:beta as beta
RUN apt update
RUN apt install -y clang
RUN rustup target add x86_64-apple-darwin
COPY --from=osxcross /osxcross /osxcross
WORKDIR /osxcross/target/bin
RUN bash -c 'for file in ./*; do ln -s file /bin/$file; done'
WORKDIR /
CMD ["/bin/bash"]

FROM instrumentisto/rust:nightly as nightly
RUN apt update
RUN apt install -y clang
RUN rustup target add x86_64-apple-darwin
COPY --from=osxcross /osxcross /osxcross
WORKDIR /osxcross/target/bin
RUN bash -c 'for file in ./*; do ln -s file /bin/$file; done'
WORKDIR /
CMD ["/bin/bash"]
