FROM adaickalavan/confluent-kafka-go as build-stage

#Author label
LABEL Author Adaickalavan Meiyappan

# Install runtime tools
ENV BUILD="ca-certificates \
         git \
         build-base \
         musl-dev \
         alpine-sdk \
         make \
         gcc \
         g++ \
         libc-dev \
         linux-headers \
         libjpeg-turbo \
         libpng \
         libwebp \
         libwebp-dev \
         tiff \
         libavc1394 \
         jasper-libs \
         openblas \
         libgphoto2 \
         gstreamer \
         gst-plugins-base"

ENV DEV="clang clang-dev cmake pkgconf \
         openblas-dev gstreamer-dev gst-plugins-base-dev \
         libgphoto2-dev libjpeg-turbo-dev libpng-dev \
         tiff-dev jasper-dev libavc1394-dev"


RUN apk update && \
    apk add --no-cache ${BUILD} ${DEV}

#Install the GoCV package
RUN go get -u -d gocv.io/x/gocv

#Change the directory into the newly installed package directory
WORKDIR $GOPATH/src/gocv.io/x/gocv

ENV PKG_CONFIG_PATH /usr/local/lib64/pkgconfig
ENV LD_LIBRARY_PATH /usr/local/lib64
ENV CGO_CPPFLAGS -I/usr/local/include
ENV CGO_CXXFLAGS "--std=c++1z"
ENV CGO_LDFLAGS "-L/usr/local/lib -lopencv_core -lopencv_face -lopencv_videoio -lopencv_imgproc -lopencv_highgui -lopencv_imgcodecs -lopencv_objdetect -lopencv_features2d -lopencv_video -lopencv_dnn -lopencv_xfeatures2d -lopencv_plot -lopencv_tracking"

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