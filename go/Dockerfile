from alpine:3.10 as bootstrap

add https://golang.org/dl/go1.12.9.src.tar.gz /go.src.tgz
env SRC_HASH ab0e56ed9c4732a653ed22e232652709afbf573e710f56a07f7fdeca578d62fc
env GOOS linux
env GOARCH amd64
env GOROOT /root/go

run apk add --no-cache bash gcc go musl-dev \
 && echo "$SRC_HASH  go.src.tgz" |sha256sum -c - \
 && tar -C /root -xf go.src.tgz \
 && cd /root/go/src \
 && ./bootstrap.bash \
 && /root/go-linux-amd64-bootstrap/bin/go version \
 && GOROOT_BOOTSTRAP=/root/go-linux-amd64-bootstrap ./make.bash \
 && /root/go/bin/go version


from alpine:3.10

copy --from=bootstrap /root/go /usr/local/go
run mkdir -p /go/bin
env GOPATH /go
env PATH "/usr/local/go/bin:$PATH:$GOPATH/bin"
run apk add --no-cache ca-certificates gcc git musl-dev
# assume go modules
workdir /src
