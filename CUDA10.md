1) Add PPA:
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```
2) Install drivers (need >=410):
```
sudo apt-get install nvidia-410
```
3) The CUDA runfile installer can be downloaded from NVIDIA’s website. Choose the runfile option:

https://developer.nvidia.com/cuda-downloads

What you download is a package the following three components:

a)an NVIDIA driver installer, but usually of stale version;
b)the actual CUDA installer;
c)the CUDA samples installer;

4) extract the above three components and executing 2 and 3 separately (remember we installed the driver ourselves already). To extract them, execute the runfile installer with --extract option:
```
chmod +x cuda_version_linux-run
./cuda_version_linux-run --extract=$HOME
```
5) Execute the second one to install the CUDA Toolkit 10.0:
```
sudo ./cuda-linux.version.run
```
6) After the installation finishes, you must configure the runtime library:
```
sudo bash -c "echo /usr/local/cuda/lib64/ > /etc/ld.so.conf.d/cuda.conf"
sudo ldconfig
```
7) It is also recommended for Ubuntu users to append string /usr/local/cuda/bin to system file /etc/environment so that nvcc will be included in $PATH. This will take effect after reboot. To do that, you just have to:
```
sudo vim /etc/environment
```
or
```
sudo nano /etc/environment
```
8) Then add :/usr/local/cuda/bin (including the ":") at the end of the PATH="/blah:/blah/blah" string (inside the quotes)

9) reboot

troubleshoot:

If some drivers already installed previously, uninstall using the following:
```
sudo apt-get purge nvidia-*
sudo apt-get autoremove --purge
```
see:
https://medium.com/@zhanwenchen/install-cuda-9-2-and-cudnn-7-1-for-tensorflow-pytorch-gpu-on-ubuntu-16-04-1822ab4b2421
for more info



