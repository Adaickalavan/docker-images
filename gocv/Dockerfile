# Start from a Debian image with the latest version of GO 
# installed and a workspace (GOPATH) configured at /go.
FROM golang:latest as build-stage

#Author label
LABEL Author Adaickalavan Meiyappan

# Install runtime tools
RUN apt-get update
RUN apt-get install build-essential sudo -y

#Install the GoCV package
RUN go get -u -d gocv.io/x/gocv

#Change the directory into the newly installed package directory
WORKDIR $GOPATH/src/gocv.io/x/gocv

# Quick install OpenCV 4.0.0 on Linux container
RUN make install

#Run the app command by default when the container starts
ENTRYPOINT ["go", "run", "./cmd/version/main.go"]

#Running 
# ```
# docker run <image_name>
# ```
#
# should print the following message:
#
# ```
#gocv version: 0.18.0
#opencv lib version 4.0.0
# ```