# Caffe

## Building from scratch on Ubuntu (available for arm)

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

### Test installation
```
./data/mnist/get_mnist.sh
./examples/mnist/create_mnist.sh
# modify ./examples/mnist/lenet_solver.prototxt
time ./examples/mnist/train_lenet.sh
```
For tx1 and tk1 
```diff
diff --git a/examples/mnist/convert_mnist_data.cpp b/examples/mnist/convert_mnist_data.cpp
index 16d2809..690a98b 100644
--- a/examples/mnist/convert_mnist_data.cpp
+++ b/examples/mnist/convert_mnist_data.cpp
@@ -93,7 +93,8 @@ void convert_dataset(const char* image_filename, const char* label_filename,
     CHECK_EQ(mkdir(db_path, 0744), 0)
         << "mkdir " << db_path << "failed";
     CHECK_EQ(mdb_env_create(&mdb_env), MDB_SUCCESS) << "mdb_env_create failed";
-    CHECK_EQ(mdb_env_set_mapsize(mdb_env, 1099511627776), MDB_SUCCESS)  // 1TB
+    //CHECK_EQ(mdb_env_set_mapsize(mdb_env, 1099511627776), MDB_SUCCESS)  // 1TB
+    CHECK_EQ(mdb_env_set_mapsize(mdb_env, 536870912), MDB_SUCCESS)
         << "mdb_env_set_mapsize failed";
     CHECK_EQ(mdb_env_open(mdb_env, db_path, 0, 0664), MDB_SUCCESS)
         << "mdb_env_open failed";
diff --git a/src/caffe/util/db_lmdb.cpp b/src/caffe/util/db_lmdb.cpp
index 0bc82b5..35aebd3 100644
--- a/src/caffe/util/db_lmdb.cpp
+++ b/src/caffe/util/db_lmdb.cpp
@@ -7,7 +7,9 @@
 
 namespace caffe { namespace db {
 
-const size_t LMDB_MAP_SIZE = 1099511627776;  // 1 TB
+//const size_t LMDB_MAP_SIZE = 1099511627776;  // 1 TB
+const size_t LMDB_MAP_SIZE = 536870912; // 2^29. fix for Jetson TK1
```

#### Mac Dependency
```
brew install --build-from-source --with-python -vd protobuf
brew install -vd snappy leveldb gflags glog szip lmdb openblas
```
edit Makefile.config.example to remove GPU and customize using opencv 3.0  
CMake is not recommand to use on Max OSX platform  
You may find python include/lib direcoty path is something like this:
`/usr/local/Cellar/python/2.7.10_2/Frameworks/Python.framework/Versions/2.7/include/python2.7/`


#### Installing on 16.04 (may or may not be true)
```
#opencv dependency
#change Makefile line ~164
LIBRARIES += glog gflags protobuf leveldb snappy \
  lmdb boost_system hdf5_hl hdf5 m \
  opencv_core opencv_highgui opencv_imgproc opencv_imgcodecs
```
```
#hdf5
#Edit Makefile.conf
PYTHON_INCLUDE := /usr/include/python2.7 /usr/lib/python2.7/dist-packages/numpy/core/include

WITH_PYTHON_LAYER := 1

INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial

LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu /usr/lib/x86_64-linux-gnu/hdf5/serial
```
See [here](https://github.com/BVLC/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide)for more details.
