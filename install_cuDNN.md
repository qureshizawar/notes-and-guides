taken from https://askubuntu.com/questions/767269/how-can-i-install-cudnn-on-ubuntu-16-04


Step 0: Install cuda from the standard repositories. (See How can I install CUDA on Ubuntu 16.04?)

Step 1: Register an nvidia developer account and download cudnn here (about 80 MB)

Step 2: Check where your cuda installation is. For the installation from the repository it is /usr/lib/... and /usr/include. Otherwise, it will be /usr/local/cuda/ or /usr/local/cuda-<version>. You can check it with which nvcc or ldconfig -p | grep cuda

Step 3: Copy the files:

Repository installation:
```
$ cd folder/extracted/contents
$ sudo cp -P include/cudnn.h /usr/include
$ sudo cp -P lib64/libcudnn* /usr/lib/x86_64-linux-gnu/
$ sudo chmod a+r /usr/lib/x86_64-linux-gnu/libcudnn*
```
Runfile installation:
```
$ cd folder/extracted/contents
$ sudo cp include/cudnn.h /usr/local/cuda/include
$ sudo cp lib64/libcudnn* /usr/local/cuda/lib64
$ sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```