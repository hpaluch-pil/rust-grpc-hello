# Finsihed gRPC Rust tutorial

Here is finished gRPC Rust tutorial
from:
- https://github.com/hyperium/tonic/blob/master/examples/helloworld-tutorial.md

## Setup: openSUSE LEAP 15.3

Install these packages:
```bash
sudo zypper in cmake make gcc glibc-devel g++ rustup git-core
```

NOTE: cmake and g++ is required by `prost` (builds protobuf generator written in C++)

If you did not setup `rustup` yet run:
```bash
rustup-init
```
- confirm default install
- you may need to reload your shell environment
  using command like `source ~/.bashrc`
- here are my versions:

```bash
$ lsb_release -d

Description:	openSUSE Leap 15.3

$ rustc -V

rustc 1.60.0 (7737e0b5c 2022-04-04)

$ cargo -V

cargo 1.60.0 (d1fd9fe 2022-03-01)

$ rustup toolchain list

stable-x86_64-unknown-linux-gnu (default)
```

Now you can checkout this project:
```bash
mkdir -p ~/projects
cd ~/projects
git clone xxxxxx
cd ../grpc-hello/
```

Now build this project:
```bash
cargo build
```
It make take quite long, because the `prost` compiles C++ protobuf generator.
In my case (4 core Celeron N3450) it took about 13 minutes to build.

In one terminal run server:
```bash
cargo run --bin helloworld-server
```

Once it starts in another terminal run client:
```bash
cargo run --bin helloworld-client
```

If everything works properly you should see on Client terminal message:
```
ESPONSE=Response { metadata: MetadataMap { headers:
   {"content-type": "application/grpc", "date": "Thu, 21 Apr 2022 06:58:49 GMT",
    "grpc-status": "0"} }, message: HelloReply {
      message: "Hello Tonic!" }, extensions: Extensions }
```

And also on server terminal:
```
Got a request: Request { metadata: MetadataMap { headers: 
  {"te": "trailers", "content-type": "application/grpc", "user-agent": "tonic/0.7.1"} },
    message: HelloRequest { name: "Tonic" }, extensions: Extensions }
```

If you are curious how those Rust bindings (and other code) looks you can
view generated code like this:
```
target/debug/build/grpc-hello-5b45552c0b2261f6/out/helloworld.rs
```

# Resources

gRPC Hello tutorial page:
- https://github.com/hyperium/tonic/blob/master/examples/helloworld-tutorial.md

