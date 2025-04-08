# https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel_22-04.html
# FROM nvcr.io/nvidia/pytorch:22.04-py3

# RUN conda install -y -c openbabel openbabel
# RUN conda install -y -c dglteam dgl-cuda11.6
# RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
# COPY ./requirements.txt /app/requirements.txt
# RUN pip install -r /app/requirements.txt

# COPY ./lib/pydock-0.4-cp38-cp38-manylinux_2_31_x86_64.whl /app/pydock-0.4-cp38-cp38-manylinux_2_31_x86_64.whl
# RUN pip install /app/pydock-0.4-cp38-cp38-manylinux_2_31_x86_64.whl


# https://docs.nvidia.com/deeplearning/frameworks/pytorch-release-notes/rel_22-09.html
BootStrap: docker
From: nvcr.io/nvidia/pytorch:22.09-py3

%post
# Install Python Requirements
pip install  dgl -f https://data.dgl.ai/wheels/cu118/repo.html
# RUN pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
mkdir /app
cd /app
wget https://raw.githubusercontent.com/truatpasteurdotfr/CarsiDock/refs/heads/main/requirements.txt
pip install -r /app/requirements.txt

# Install build-essential
apt-get update && apt-get install -y build-essential

# Install pydock
cd /app && git clone https://github.com/gitabtion/dockcpp.git
cd /app/dockcpp && mkdir build && cd build && \
        cmake .. && make install-python-package && \
        cd ../../

# Install OpenBabel
cd /app && git clone https://github.com/openbabel/openbabel.git
cd /app/openbabel && mkdir build && cd build && \
    cmake .. -DPYTHON_BINDINGS=ON && make && make install && \
    cd ../../
apt-get update && apt-get install -y swig
pip install openbabel
