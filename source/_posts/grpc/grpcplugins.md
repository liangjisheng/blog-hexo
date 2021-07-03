---
title: grpc plugins not support
date: 2021-05-18 20:18:00
tags:
---

起因是执行 protoc 报下面的错误

```sh
--go_out: protoc-gen-go: plugins are not supported; use 'protoc --go-grpc_out=...' to generate gRPC
```

原因是2个不同包下面的 protoc-gen-go 导致的, 更多详细情况查看 [issue](https://github.com/golang/protobuf/issues/1070)
