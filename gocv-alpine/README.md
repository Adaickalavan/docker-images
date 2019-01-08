# GoCV-Alpine 3.7 and OpenCV 4.0

## What's in build-stage image?

 - Alpine 3.7
 - FFMPEG 4.0
 - Golang 1.10
 - OpenCV 4.0.0
 - OpenCV 4.0.0 contrib packages required by GoCV

## What's in runtime image?

 - Alpine 3.7
 - Whatever you need there

## Purpose

This is a build image for the multi-stage image provisioning as well as runtime image to work with gocv-based binaries.

## Example

Sample Docker file you can find [here](example/Dockerfile).

## Build the runtime image

```bash
pushd runtime && docker build -t adaickalavan/gocv-alpine:4.0.0-runtime .; popd
```

## Build the build-stage image

```bash
pushd build-stage && docker build -t adaickalavan/gocv-alpine:4.0.0-buildstage .; popd
```

## Test sample:

```bash
pushd example && docker build -t adaickalavan/gocv-alpine:test .; popd
```
```bash
docker run --rm -ti adaickalavan/gocv-alpine:test
```

the output should be the following:
```bash
gocv version: 0.18.0
opencv lib version: 4.0.0
```