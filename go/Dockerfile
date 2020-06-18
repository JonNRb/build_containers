from alpine:3.12 as bootstrap

add https://golang.org/dl/go1.14.4.src.tar.gz /go.src.tgz
env SRC_HASH 7011af3bbc2ac108d1b82ea8abb87b2e63f78844f0259be20cde4d42c5c40584
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


from alpine:3.12

copy --from=bootstrap /root/go /usr/local/go
run mkdir -p /go/bin
env GOPATH /go
env PATH "/usr/local/go/bin:$PATH:$GOPATH/bin"
run apk add --no-cache ca-certificates gcc git musl-dev
# assume go modules
workdir /src
