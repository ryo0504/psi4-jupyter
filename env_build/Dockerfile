FROM ubuntu:latest

# install linux commands
RUN apt-get update && apt-get install -y \
    sudo \
    wget \
    vim \
    curl \
    unzip

# add Japanese packages to ubuntu
RUN apt-get install -y language-pack-ja-base language-pack-ja \
fontconfig fonts-takao && locale-gen ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8

# install miniconda3-py3.6
WORKDIR /opt
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-4.5.4-Linux-x86_64.sh && \
sh /opt/Miniconda3-4.5.4-Linux-x86_64.sh -b -p /opt/miniconda3 && \
rm -f Miniconda3-4.5.4-Linux-x86_64.sh

# set path
ENV PATH /opt/miniconda3/bin:$PATH


# install libraries
RUN pip install --upgrade pip && \
conda update -n base conda && \
apt-get -y install openbabel && \
conda install psi4 psi4-rt python=3.7 -c psi4 && \
conda install -c conda-forge rdkit && \
pip install openfermion && \
pip install py3Dmol && \
pip install pubchempy && \
conda install -c conda-forge nodejs jupyterlab

WORKDIR /

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--allow-root", "--LabApp.token=''"]