# Caffe

## Building from scratch (available for arm)

### Install protobuf
```
sudo apt-get install build-essential make cmake autoconf automake libtool libatlas-base-dev libsnappy-dev libleveldb-dev liblmdb-dev libboost-all-dev libhdf5-dev
git clone https://github.com/google/protobuf.git #v3.0.0-beta-2
cd protobuf
./autogen.sh 
./configure
sudo make -j install
```

### Install Caffe
```
git clone https://github.com/BVLC/caffe #rc3
mkdir caffe/build
cd caffe/build
cmake ..
sudo make -j install
```
