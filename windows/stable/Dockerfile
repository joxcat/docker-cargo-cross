FROM rust:1.43.1

RUN apt update
RUN apt install -y gcc-mingw-w64

RUN rustup target add x86_64-pc-windows-gnu

CMD ["/bin/sh"]