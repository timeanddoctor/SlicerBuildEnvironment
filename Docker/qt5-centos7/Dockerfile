FROM dockbuild/centos7:latest

ARG IMAGE
ENV DEFAULT_DOCKCROSS_IMAGE=${IMAGE}

ARG DEBIAN_FRONTEND=noninteractive

RUN \
  #
  # Qt dependencies: https://doc.qt.io/qt-5/linux-requirements.html
  #
  yum install -y \
    fontconfig \
    freetype \
    glib2 \
    libX11 \
    libxcb \
    libXi \
    libXext \
    libXrender \
    libSM \
    libICE \
    xcb-util-keysyms \
    xcb-util-image \
    libGLU-devel \
    mesa-libOSMesa-devel \
    mesa-libGL-devel \
    mesa-libGLU-devel

ENV PATH=/opt/qt/5.10.1/gcc_64/:${PATH}
ADD qt-installer-noninteractive.qs /usr/src/qt-installer-noninteractive.qs

RUN \
  cd /usr/src && \
  curl -LO http://download.qt.io/official_releases/online_installers/qt-unified-linux-x64-online.run && \
  chmod u+x qt-unified-linux-x64-online.run && \
  ./qt-unified-linux-x64-online.run --verbose --platform minimal --script ./qt-installer-noninteractive.qs && \
  rm -f qt-installer-noninteractive.qs qt-unified-linux-x64-online.run

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG IMAGE
ARG VCS_REF
ARG VCS_URL
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name=$IMAGE \
      org.label-schema.description="Base image for slicer/slicer-builds-deps and slicer/slicer-build" \
      org.label-schema.url="http://www.slicer.org" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url=$VCS_URL \
      org.label-schema.schema-version="1.0" \
      maintainer="3D Slicer Community <slicer-devel@bwh.harvard.edu>"