FROM --platform=linux/amd64 ubuntu:22.04 AS builder

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y build-essential cmake git

COPY . /repo
WORKDIR /repo/build
RUN cmake .. -DBUILD_SHARED_LIBS=ON -DOPENDRIVE_BUILD_TESTS=ON
RUN make -j$(nproc)

FROM ubuntu:22.04 AS package

COPY --from=builder /repo/build/libOpenDrive.so /deps/
COPY --from=builder /repo/build/tests /repo/build/tests
ENV LD_LIBRARY_PATH=/deps
