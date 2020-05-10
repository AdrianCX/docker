FROM ubuntu:18.04

LABEL "Maintainer"="Adrian Cruceru cruceruadrian@gmail.com"

ARG DEBIAN_FRONTEND=noninteractive

WORKDIR /setup/

RUN apt-get update && apt-get install -y wget curl build-essential g++ clang pkg-config libssl-dev protobuf-compiler git emacs gdb xclip
RUN git clone https://github.com/AdrianCX/emacs.git && cp ./emacs/.emacs ~/ && cp -r ./emacs/emacs ~/ && echo "alias em='emacs -nw'" >> ~/.bashrc

RUN wget https://sh.rustup.rs -O ./rust.sh && chmod u+x ./rust.sh && ./rust.sh -y && echo "source ~/.cargo/env" >> ~/.bashrc
RUN bash -c "source ~/.cargo/env && rustup toolchain add nightly && rustup default nightly && rustup component add rust-src"

CMD ["/bin/bash/"]