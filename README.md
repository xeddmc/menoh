# Menoh

[![travis](https://img.shields.io/travis/pfnet-research/menoh/master.svg)](https://travis-ci.org/pfnet-research/menoh) [![Build status](https://ci.appveyor.com/api/projects/status/luo2m9p5fg9jxjsh/branch/master?svg=true)](https://ci.appveyor.com/project/pfnet-research/menoh/branch/master)

Menoh is DNN inference library with C API.

Menoh is released under MIT License.

DISCLAIMER: Menoh is still experimental. Use it at your own risk.
In particular not all operators in ONNX are supported, so please check whether the operators used in your model are supported. We have checked that VGG16 and ResNet50 models converted by onnx-chainer work fine.

[Document](https://pfnet-research.github.io/menoh/)

This codebase contains C API and C++ API.

For Windows users, prebuild libraries are available (see [release](https://github.com/pfnet-research/menoh/releases)) and Nuget package is [available](https://www.nuget.org/packages/Menoh/).

See also
- Chainer model to ONNX : [onnx-chainer](https://github.com/chainer/onnx-chainer)
- C# wrapper : [menoh-sharp](https://github.com/pfnet-research/menoh-sharp)
- Go wrapper : [go-menoh](https://github.com/pfnet-research/go-menoh)
  - (unofficial wrapper [gomenoh](https://github.com/kou-m/gomenoh) by kou-m san has been merged)
- Haskell wrapper : [menoh-haskell](https://github.com/pfnet-research/menoh-haskell)
- Ruby wrapper : [menoh-ruby](https://github.com/pfnet-research/menoh-ruby)
- [Unofficial] Rust wrapper by Y-Nak san : [menoh-rs](https://github.com/Y-Nak/menoh-rs)
- [Unofficial] Rust wrapper by Hakuyume san : [menoh-rs](https://github.com/Hakuyume/menoh-rs)
- [Unofficial] ROS interface : [menoh_ros](https://github.com/akio/menoh_ros)

## Goal

- DNN Inference with CPU
- ONNX support
- Easy to use.

# Requirements

- MKL-DNN Library (0.14 or later)
- Protocol Buffers (3.5.1 is checked)

# Build

Execute below commands in root directory.

```
python retrieve_data.py
mkdir build && cd build
cmake ..
make
```

# Installation

Execute below command in build directory created at Build section.

```
make install
```

# Run VGG16 example

Execute below command in root directory.

```
./example/vgg16_example_in_cpp
```

Result is below

```
vgg16 example
-22.3708 -34.4082 -10.218 24.2962 -0.252342 -8.004 -27.0804 -23.0728 -7.05607 16.1343
top 5 categories are
8 0.96132 n01514859 hen
7 0.0369939 n01514668 cock
86 0.00122795 n01807496 partridge
82 0.000225824 n01797886 ruffed grouse, partridge, Bonasa umbellus
97 3.83677e-05 n01847000 drake
```

Please give `--help` option for details

```
./example/vgg16_example_in_cpp --help
```


# Run test

Setup chainer

Then, execute below commands in root directory.

```
python gen_test_data.py
cd build
cmake -DENABLE_TEST=ON ..
make
./test/menoh_test.out
```

# Current supported operators

### Activation functions
- Elu
- LeakyRelu
- Relu
- Softmax
- Tanh

### Array manipulations
- Concat

### Neural network connections
- Conv
- ConvTranspose
- FC

### Mathematical functions
- Abs
- Add
- Sqrt

### Normalization functions
- BatchNormalization

### Spatial pooling
- AveragePool
- GlobalAveragePool
- GlobalMaxPool
- MaxPool

# License

Menoh is released under MIT License. Please see the LICENSE file for details.

Note: `retrieve_data.py` downloads `data/VGG16.onnx`. `data/VGG16.onnx` is generated by onnx-chainer from pre-trained model which is uploaded
at http://www.robots.ox.ac.uk/%7Evgg/software/very_deep/caffe/VGG_ILSVRC_16_layers.caffemodel

That pre-trained model is released under Creative Commons Attribution License.
