FROM golang:1.22 AS build
ARG GOARCH="arm64"
ARG GOOS="linux"
ENV GOARCH=$GOARCH GOOS=$GOOS CGO_ENABLED=0
COPY . /build_dir
WORKDIR /build_dir
ENV GOPROXY=https://proxy.golang.org
RUN make clean && make benchtool

FROM       alpine:3.14
RUN        apk add --update --no-cache ca-certificates
COPY       --from=build /build_dir/cmd/benchtool/benchtool /usr/bin/benchtool
EXPOSE     9090
ENTRYPOINT [ "/usr/bin/benchtool" ]
