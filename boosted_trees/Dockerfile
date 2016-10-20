FROM nvidia/cuda:latest

RUN apt-get update && apt-get install -y firefox
RUN apt-get install libcanberra-gtk3-module -y
# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

USER developer
ENV HOME /home/developer
CMD /usr/bin/firefox

RUN sudo apt-get git
RUN sudo apt-get mercurial
RUN sudo apt-get install libopencv-dev build-essential checkinstall cmake pkg-config -y
RUN sudo apt-get install yasm libtiff4-dev libjpeg-dev libjasper-dev libavcodec-dev -y
RUN sudo apt-get install libavformat-dev libswscale-dev libdc1394-22-dev libxine-dev -y
RUN sudo apt-get install libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev -y
RUN sudo apt-get install python-dev python-numpy libtbb-dev libqt4-dev libgtk2.0-dev -y
RUN sudo apt-get install libmp3lame-dev libopencore-amrnb-dev -y
RUN sudo apt-get install libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils -y
RUN sudo apt-get install cuda -y

RUN sudo apt-get install software-properties-common -y
RUN sudo add-apt-repository ppa:george-edison55/cmake-3.x
RUN sudo apt-get update
RUN sudo apt-get install cmake -y

RUN sudo apt-get install qt5-default -y

RUN cd ~
RUN mkdir OpenCV
RUN cd OpenCV
RUN git clone https://github.com/Itseez/opencv.git

RUN cd opencv
RUN mkdir release
RUN cd release
RUN cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D ENABLE_FAST_MATH=1 -D CUDA_FAST_MATH=1 -D WITH_CUBLAS=1 ..
