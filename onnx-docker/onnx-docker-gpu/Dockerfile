# Using this script to build your ONNX image.
# Execute "docker build dir", where dir contains this Dockerfile. Make sure you give docker container at least 8GB memory.
# Execute "docker run -i -t image_id", where image_id is the id of the image you just generated.
# Try "python tutorial-without-mobile-part.py".

FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

RUN echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1604/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list

RUN apt-get update && apt-get install -y software-properties-common

RUN add-apt-repository ppa:deadsnakes/ppa

RUN apt-get update && apt-get install -y --no-install-recommends \
         build-essential \
         cmake \
         git \
         ssh \
         vim \
         curl \
         ca-certificates \
         wget \
         unzip \
         libjpeg-dev \
         libpng-dev \
	 libgflags-dev \
         libgoogle-glog-dev \
         liblmdb-dev \
         libprotobuf-dev \
         protobuf-compiler \
         cmake \
         python3.6 python3-pip python3-dev python3-setuptools && \
     rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip
RUN pip3 install wheel ipython==5.0 numpy scipy pyyaml scipy scikit-learn numpy

RUN mkdir -p /root/programs
RUN git clone --recursive https://github.com/onnx/onnx.git /root/programs/onnx
RUN git clone --recursive https://github.com/pytorch/pytorch.git /root/programs/pytorch
RUN cd /root/programs/onnx; python3 setup.py install

RUN pip3 install --user \
    	 future \
  	 leveldb \
   	 numpy \
   	 protobuf \
  	 pydot \
  	 python-gflags \
    	 pyyaml \
   	 scikit-image \
   	 six

RUN cd /root/programs/pytorch; mkdir build && cd build; cmake ..; make install

WORKDIR /root/programs
