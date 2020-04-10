# AI-learning-source
My AI Learning
### [nvidia-jetson-nano-tensorflow-gpu](http://asahinow.blogspot.com/2019/08/nvidia-jetson-nano-tensorflow.html)
### ubuntu 下 python及pip 安装whl文件常见问题汇总

### 1.安装python

**1）\**no acceptable C compiler found in $PATH when installing python\****

  解决方法：

  系统基于redhat，则:

  ***\*yum groupinstall "Development tools"\****

 系统基于Debian :

  ***\*apt-get install build-essential\****

**2）****ubuntu E: Package 'libpng12-dev'或者E: Package 'libjpeg8-dev' has no installation candidate**
**has no installation candidate**

  解决方法：

  **libpng12-dev在Ubuntu16.04之后就被丢弃了，所以放弃用这个吧**

   ***\*把libpng12-dev换成libpng-dev就行了。同理 jpeg也适用。\****

### **2.安装 scipy:**

**1）出现 \**no lapack/blas sources found\** 错误.**

  解决方法：

  ***\*sudo apt-get install libblas-dev liblapack-dev libatlas-base-dev gfortran\****

 

#### **3.安装Pillow:**

**1）出现** ***\*The headers or library files could not be found for jpeg,  a required dependency when compiling Pillow from source.\******错误。**

解决方法：这是pillow 3及以上就需要 “libjpeg”，因此需要安装相关依赖。

```html
sudo apt-get install libtiff5-dev libjpeg-dev libopenjp2-7-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev tk8.6-dev python-tk libharfbuzz-dev libfribidi-dev
```

#### **4.安装H5py**

**1）\**pip install h5py 下载完成后卡住不动：\****

 解决方法：

 ***\*sudo pip3 install cython
 sudo apt-get install libhdf5-dev
 sudo pip3 install h5py\****
