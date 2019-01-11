# Start from a Debian image with the latest version of GO 
# installed and a workspace (GOPATH) configured at /go.
FROM golang:latest

#Author label
LABEL Author Adaickalavan Meiyappan

# Install runtime tools
RUN apt-get update && \
    apt-get install build-essential \
    ffmpeg \
    gstreamer1.0-* \
    libgstreamer1.0-0 \
    libgtk2.0-dev \
    pkg-config \
    sudo -y

    # gstreamer1.0-plugins-base \
    # gstreamer1.0-plugins-good \
    # gstreamer1.0-plugins-bad \
    # gstreamer1.0-plugins-ugly \
    # gstreamer1.0-libav \
    # gstreamer1.0-doc \
    # gstreamer1.0-tools \
    # gstreamer1.0-x \
    # gstreamer1.0-alsa \
    # gstreamer1.0-gl \
    # gstreamer1.0-gtk3 \
    # gstreamer1.0-qt5 \
    # gstreamer1.0-pulseaudio \

#Install the GoCV package
RUN go get -u -d gocv.io/x/gocv

#Change the directory into the newly installed package directory
WORKDIR $GOPATH/src/gocv.io/x/gocv

# Quick install OpenCV 4.0.0 on Linux container
RUN make install

# To verify that the Docker image has been built correctly, do the following.
# By enabling the ENTRYPOINT command below, running 
# ```
# docker run <image_name>
# ```
#
# should print the following message:
#
# ```
#gocv version: 0.18.0
#opencv lib version 4.0.0
# 

# Run the app command by default when the container starts
# ENTRYPOINT ["go", "run", "./cmd/version/main.go"]
