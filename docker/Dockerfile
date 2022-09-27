FROM gitpod/workspace-full

#RUN sudo apt-get update && \

USER gitpod

RUN brew install httpie && \
    brew install bat && \
    brew install exa && \
    brew install hey

# ------------------------------------
# Install TinyGo
# ------------------------------------
ARG TINYGO_VERSION="0.25.0"
RUN wget https://github.com/tinygo-org/tinygo/releases/download/v${TINYGO_VERSION}/tinygo_${TINYGO_VERSION}_amd64.deb
RUN sudo dpkg -i tinygo_${TINYGO_VERSION}_amd64.deb
RUN rm tinygo_${TINYGO_VERSION}_amd64.deb

# ------------------------------------
# Install Rust support
# ------------------------------------
RUN rustup toolchain uninstall stable-x86_64-unknown-linux-gnu && \
    curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh -s -- -y && \
    curl https://rustwasm.github.io/wasm-pack/installer/init.sh -sSf | sh && \
    rustup target add wasm32-wasi

# ------------------------------------
# Install Subo
# ------------------------------------

RUN brew tap suborbital/subo && \
    brew install subo

# ------------------------------------
# Install Sat (Suborbital)
# ------------------------------------
RUN git clone --depth=1 https://github.com/suborbital/sat.git && \
    cd sat && \
    go build -o .bin/sat -tags netgo,wasmtime . && \
    sudo cp .bin/sat /usr/local/bin/sat && \
    cd .. && \
    rm -rf sat

# ------------------------------------
# Install E2Core (Suborbital)
# ------------------------------------
RUN git clone https://github.com/suborbital/e2core.git
RUN cd e2core && \
    make e2core/install && \
    cd .. && \
    rm -rf e2core

