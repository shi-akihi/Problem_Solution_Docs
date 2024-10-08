# Setting Environment

## gcc DSO Problem

### Problem
```
 /usr/bin/ld: CMakeFiles/fakeio_node.dir/rclcpp_components/node_main_fakeio_node.cpp.o: undefined reference to symbol '_ZSt20__throw_length_errorPKc@@GLIBCXX_3.4'
 /usr/bin/ld: /lib/x86_64-linux-gnu/libstdc++.so.6: error adding symbols: DSO missing from command line
```

### Solution
```shell
# remove and reinstall gcc 
sudo apt remove gcc-11
sudo apt remove build-essential
sudo apt autoremove
sudo apt install build-essential
```

## Can't find NvInfer.h problem

### Problem
```
fatal error: NvInfer.h: No such file or directory
   10 | #include <NvInfer.h>
```

### Solution
```bash
# add the TensorRT include path in ~/.bashrc as follow
export CPATH=/usr/local/tensorrt/include:$CPATH
```

## Can't find cuda/tensorrt in cmake

### Problem
```
/usr/bin/ld:cannot find -lcuda: No such file or directory
```

### Solution
```bash
# add the path to both ld_library_path and library_path
# wsl for example
export LIBRARY_PATH=/usr/lib/wsl/lib:$LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/lib/wsl/lib:$LD_LIBRARY_PATH
```

## gpg key error in change apt source list 

### Problem 
```
W: GPG error: http://mirrors.tuna.tsinghua.edu.cn/ubuntu xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
E: The repository 'http://mirrors.tuna.tsinghua.edu.cn/ubuntu xenial InRelease' is not signed.
```

### Solution
```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 40976EAF437D05B5
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
```

May cause warning when run `sudo apt update`, which can be solved by the following commands. 

```bash
cd /etc/apt
sudo cp trusted.gpg trusted.gpg.d
```

