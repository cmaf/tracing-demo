# Kata Containers runtime tracing

Updated documentation for tracing is found in the Kata Containers [tracing document PR](https://github.com/kata-containers/kata-containers/pull/1937/files).  

## Enable tracing in configuration file

```
[runtime]
enable_tracing = true
```

## Run Jaeger All-in-one container

[Jaeger All-in-one](https://www.jaegertracing.io/docs/1.23/getting-started/#all-in-one) launches the trace collector and UI.

```
$ docker run -d --name jaeger \
  -e COLLECTOR_ZIPKIN_HOST_PORT=:9411 \
  -p 5775:5775/udp \
  -p 6831:6831/udp \
  -p 6832:6832/udp \
  -p 5778:5778 \
  -p 16686:16686 \
  -p 14268:14268 \
  -p 14250:14250 \
  -p 9411:9411 \
  jaegertracing/all-in-one:1.23
  ```

## Run container and get trace

```
$ sudo ctr run --runtime "io.containerd.kata.v2" --rm -t "docker.io/library/busybox:latest" test sh
```
