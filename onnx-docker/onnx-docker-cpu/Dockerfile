# Using this script to build your ONNX image.
# Execute "docker build dir", where dir contains this Dockerfile. Make sure you give docker container at least 8GB memory.
# Execute "docker run -i -t image_id", where image_id is the id of the image you just generated.
# Try "python tutorial-without-mobile-part.py".

FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

# download conda
RUN mkdir -p /root/programs
RUN ["/bin/bash", "-c", "wget https://repo.continuum.io/archive/Anaconda3-latest-Linux-x86_64.sh -O /root/programs/anaconda.sh"]
RUN chmod 0755 /root/programs/anaconda.sh
RUN ["/bin/bash", "-c", "/root/programs/anaconda.sh -b -p /root/programs/anaconda3"]
ENV PATH="/root/programs/anaconda3/bin:$PATH"
RUN rm /root/programs/anaconda.sh
    
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
         cmake && \
     rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip
RUN pip install wheel ipython==5.0 numpy scipy pyyaml scipy scikit-learn numpy future levelldb protobuf pytdot python-gflags scikit-image six

RUN git clone --recursive https://github.com/onnx/onnx.git /root/programs/onnx
RUN git clone --recursive https://github.com/pytorch/pytorch.git /root/programs/pytorch
RUN cd /root/programs/onnx; python setup.py develop

RUN cd /root/programs/pytorch; mkdir build && cd build; cmake ..; make install

RUN cd /root/programs/pytorch; pip install -r "requirements.txt"; \
    NO_CUDA=0 python setup.py build develop

WORKDIR /root/programs
