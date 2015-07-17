---
layout: post
title: "DeepDream"
date: "2015-07-17"
---
# Running Google's DeepDream
No cognitivist could avoid noticing google's new demonstrations on Deep Learning posted on their [research blog](http://googleresearch.blogspot.mx/2015/06/inceptionism-going-deeper-into-neural.html) this june. Images all over the web like those on google's own [gallery](https://photos.google.com/share/AF1QipPX0SCl7OzWilt9LnuQliattX4OUCj_8EP65_cTVnBmS1jnYgsGQAieQUc1VQWdgQ?key=aVBxWjhwSzg2RjJWLWRuVFBBZEN1d205bUdEMnhB) showing what neural networks "see" when trying to make sense of images make everyone wonder how could a machine make such beautiful, weird, and surprisingly familiar images.

In fact so many people from so many different backgrounds, from scientists to artists, have been so interested in google's deepdreaming that the company decided to open their code. The repo can now be found as an IPython notebook on [github](https://github.com/google/deepdream) so anyone and everyone can have their own deeplearning nerual network. Well, not really everyone. The process of installing and running a deeplearning system is not for everyone. For someone trying to do it on an OSx system, for example, it might seem imposible at the time due to so many dependencies.

Fortunately, linux has not much problems with dependencies. I hadn't actually thought on trying linux. Usually when a project cannot be compiled on mac I tend to leave it aside and work my way arround, but this time, the temptation was much. With the help of my friend [Diego Montesinos](https://github.com/diegoMontesinos), who pointed me to [a post on Redit](https://www.reddit.com/r/deepdream/comments/3cd1yf/howto_install_on_ubuntulinux_mint_including_cuda/) I was able to install and run the DeepDream library on a Debian Jessie. I have no special hardware so I used no CUDA specs. The recipie is the following:

## Dependencies
The first step is to get dependencies running. The most relevant of these is Caffe: an open source deep learning library. Python and Numpy are also needed, as well as Google's protobuf library for buffering prototipes.

```
sudo apt-get install build-essential git
git clone https://github.com/BVLC/caffe.git
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev python python-dev python-scipy python-setuptools python-numpy python-pip libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler libatlas-dev libatlas-base-dev libatlas3-base libatlas-test
sudo apt-get install --no-install-recommends libboost-all-dev
sudo pip install --upgrade pip
sudo pip install --upgrade numpy
cd caffe
```
Before compiling caffe we must configure it for the specific requirements:
```
cp Makefile.config.example Makefile.config
```
With our prefered text editor there are a couple things to do:
- Uncomment `CPU_ONLY := 1` since CUDA is not being used.
- Add the included directories and libraries for hdf5

```
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/

LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/
```

Once this has been done we must add the libraries to our path. We can do so by writing the following lines on `~/.bashrc`:

```
export LD_LIBRARY_PATH=/usr/local/lib
export PYTHONPATH="${PYTHONPATH}:/home/abcsds/caffe/python"
```
Don't forget to source it: `source ~/.bashrc`.
## Building Caffe
Now that Caffe's dependencies have been met, build by typing the following code in the Caffe project folder(replaceing x by the number of cores yout processor has):
```
make all -jx
make test -jx
make runtest -jx
make pycaffe -jx
```
## Runing DeepDream
All dependencies for the DeepDream librariy should be met by now, and we can run the code on the repo:

```
git clone https://github.com/google/deepdream.git
wget -P ~/caffe/models/bvlc_googlenet http://dl.caffe.berkeleyvision.org/bvlc_googlenet.caffemodel
cd ~/deepdream
ipython notebook ./dream.ipynb
```
This last instruction will open an IPython notebook on your browser, where you can click every snippet of code and run by clicking the play icon on the top of the content section.
