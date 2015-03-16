Introduction
================

Benchmark tool for HTTP/SPDY over QUIC protocol written in Go. Originally forked from cmpxchg16's [Gobench](https://github.com/cmpxchg16/gobench).


Getting Started
================

## Dependency

  * [goquic](https://github.com/devsisters/goquic)
  * [gospdyquic](https://github.com/devsisters/gospdyquic)

## Build static library files

To build quicbench, you should build goquic's [static library files](https://github.com/devsisters/gospdyquic#build-static-library-files).

## How to build

Due to Go 1.4's cgo restrictions, use an environment variable like below to
build your projects. This restriction will be removed from Go 1.5.

```bash
CGO_LDFLAGS="-L$GOPATH/src/github.com/devsisters/goquic/lib/$GOOS_$GOARCH"
```

For example, building quicbench in Mac:

```bash
CGO_LDFLAGS="-L$GOPATH/src/github.com/devsisters/goquic/lib/darwin_amd64" go build $GOPATH/github.com/devsisters/quicbench/quicbench.go
```

In Linux:

```bash
CGO_LDFLAGS="-L$GOPATH/src/github.com/devsisters/goquic/lib/linux_amd64" go build $GOPATH/github.com/devsisters/quicbench/quicbench.go
```

## Usage

1. run some quic supported server. You may use server implementation bundled in [gospdyquic](https://github.com/devsisters/gospdyquic)
   or toy server implementation in Chromium [here](http://www.chromium.org/quic/playing-with-quic)
2. run quicbench for HTTP GET

   ```$>go run quicbench.go -u http://localhost:80 -k=true -c 50 -r=10 -t 10```
3. run quicbench for HTTP POST

   ```$>go run quicbench.go -u http://localhost:80 -k=true -c 50 -r=10 -t 10 -d /tmp/post```


Notes
================

1. build a binary: 

    ```$>go build gobench.go```
    
2. Because it's a test tool, in HTTPS the ceritificate verification is insecure
3. use Go >= 1.1 (1.1 including major bug fixes)
4. quicbench creates one QUIC connection for each client and just create new stream for every request.
   If you want to create QUIC connection for every request, use -qk=false option.

Help
================

```go run gobench.go --help```

License
================

Licensed under the New BSD License.

Author
================

Originally written by Uri Shamay (shamayuri@gmail.com)

QUIC protocol adopted by Brian Sung-Jin Hong (sungjinhong@devsisters.com) and Joonsung Lee (joonsung@devsisters.com)
