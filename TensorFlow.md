#TensorFlow

## Installation
[Offcial Documentation](https://www.tensorflow.org/versions/master/get_started/os_setup.html#download-and-setup)
### Docker Way

```
b.gcr.io/tensorflow/tensorflow: TensorFlow CPU binary image.
b.gcr.io/tensorflow/tensorflow:latest-devel: CPU Binary image plus source code.
b.gcr.io/tensorflow/tensorflow:latest-gpu: TensorFlow GPU binary image.
b.gcr.io/tensorflow/tensorflow:latest-devel-gpu: GPU Binary image plus source code.
```

### On Mac (CPU only)
```
sudo pip install --upgrade https://storage.googleapis.com/tensorflow/mac/tensorflow-0.7.1-cp27-none-any.whl
```

### Build from scratch! (Get psyched)
[Official Documentation](https://www.tensorflow.org/versions/r0.7/get_started/os_setup.html#installing-from-sources)
This only for Ubuntu 14.04 with Nvidia GPU and CUDA&cuDNN pre-installed   
####Install Java
```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer pkg-config zip g++ zlib1g-dev unzip python-numpy swig python-dev
```
####Install bazel
```
wget https://github.com/bazelbuild/bazel/releases/download/0.2.0/bazel-0.2.0-installer-linux-x86_64.sh
chmod +x bazel-0.2.0-installer-linux-x86_64.sh
./bazel-0.2.0-installer-linux-x86_64.sh --user
echo 'export PATH="$PATH:$HOME/bin"' >> ~/.bashrc
```
####Install TensorFlow
```
 git clone --recurse-submodules https://github.com/tensorflow/tensorflow
 cd tensorflow
 ./configure
 # test building
 bazel build -c opt --config=cuda //tensorflow/cc:tutorials_example_trainer
 bazel-bin/tensorflow/cc/tutorials_example_trainer --use_gpu
 
 # build pip package
 #CPU version
 #bazel build -c opt //tensorflow/tools/pip_package:build_pip_package 
 #GPU version
 bazel build -c opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
 bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
 sudo pip install /tmp/tensorflow_pkg/tensorflow*whl
