#---
# name: python
# alias: python3
# group: build
# depends: build-essential
# notes: installs core python3 packages and pip
#---
ARG BASE_IMAGE
FROM ${BASE_IMAGE}

ENV DEBIAN_FRONTEND=noninteractive

RUN add-apt-repository ppa:deadsnakes/ppa

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
		  python3.12-dev \
		  python3-distutils \
		  python3-pip \
    && update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1 \
    && curl -sS https://bootstrap.pypa.io/get-pip.py | python3.12 \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean
    
RUN which pip3 && pip3 --version && \
    python3 -m pip install --upgrade pip

# this was causing issues downstream (e.g. Python2.7 still around in Ubuntu 18.04,
# and in cmake python enumeration where some packages expect that 'python' is 2.7)
#RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 1 && \
#    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1
    
RUN which python && python --version && pip --version && \
    which python3 && python3 --version && pip3 --version

RUN pip3 install --upgrade --no-cache-dir \
	setuptools \
	packaging \
	'Cython<3' \
	wheel
	
RUN pip3 install --no-cache-dir --verbose wget psutil
