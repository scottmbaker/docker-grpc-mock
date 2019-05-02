# Mock GRPC Server
This repository can be used to build a docker image that leverages
`grpc-mock` (`https://github.com/YoshiyukiKato/grpc-mock`) to provide
a *mock* GRPC server that can be utilized for testing.

# Usage
To utilize this image `protobuf` file(s) must be supplied as well as
a `node.js` file to create the server. There is an example in the
`example` directory.

## Example Mock Server
To run the example you can use the following docker command:
```bash
docker run -tid \
  --name mock --rm -p 50051:50051 \
  -v $(pwd)/example:/proto \
  ciena/grpc-mock /proto/mock.js
```

## Example Client
The utility `grpcurl` can be used to test the mock server using the
following command:
```bash
grpcurl -proto $(pwd)/example/greeter.proto \
  -plaintext  \
  -d '{"message": "test"}' \
  localhost:50051 greeter.Greeter/Hello
```

## Useful Environment Variables
To enable debugging information when running the mock server the following
environment variables can be set when starting the mock server container:

```bash
GRPC_VERBOSITY=DEBUG
GRPC_TRACE=all
```
