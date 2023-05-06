FROM ubuntu:16.04
RUN sed -i s:/archive.ubuntu.com:/mirrors.tuna.tsinghua.edu.cn/ubuntu:g /etc/apt/sources.list
RUN cat /etc/apt/sources.list
LABEL maintainer caffe-maint@googlegroups.com

COPY ./assets /root

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        wget \
        vim \
        libatlas-base-dev \
        libboost-all-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libopencv-dev \
        libsnappy-dev \
        libprotobuf-dev \
        protobuf-compiler && \
    rm -rf /var/lib/apt/lists/*

RUN cd /root && \
    chmod a+x Miniconda3-py38_4.8.3-Linux-x86_64.sh && \
    /bin/bash Miniconda3-py38_4.8.3-Linux-x86_64.sh -b -p /root/miniconda3 && \
    rm Miniconda3-py38_4.8.3-Linux-x86_64.sh && \
    echo 'export PATH="/root/miniconda3/bin:$PATH"' >> ~/.bashrc && \
    # source ~/.bashrc && \
    /bin/bash -c "source ~/.bashrc" && \
    cd /usr/lib/x86_64-linux-gnu/ && \
    ln -s libboost_python-py35.so.1.58.0 libboost_python3.so && \
    # cd /root/yolov5_caffe  && \
    # which -a pip && \
    /root/miniconda3/bin/pip install numpy -i https://pypi.doubanio.com/simple/  && \
    /root/miniconda3/bin/pip install scikit-image -i https://pypi.doubanio.com/simple/  && \
    /root/miniconda3/bin/pip install protobuf==3.6.1 -i https://pypi.doubanio.com/simple/  && \
    /root/miniconda3/bin/pip install onnx -i https://pypi.doubanio.com/simple/  && \
    /root/miniconda3/bin/pip install onnx-simplifier -i https://pypi.doubanio.com/simple/  && \
    cd /root/yolov5_caffe  && \
    make clean && \
    make all -j8 && \
    make pycaffe -j8
    # export PYTHONPATH=/root/yolov5_caffe/python

ENV CAFFE_ROOT=/root/yolov5_caffe
WORKDIR $CAFFE_ROOT

ENV PYCAFFE_ROOT $CAFFE_ROOT/python
ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH
# RUN echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig

WORKDIR /workspace