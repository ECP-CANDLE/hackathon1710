# Using Keras with mxnet backend

mxnet is a deep learning framework developed by Amazon, Baidu, NVidia and several other institutes. See more detail https://mxnet.incubator.apache.org/

Currently, [a fork of Keras](https://github.com/dmlc/keras) supports mxnet backend (based on Keras v1.2.2)

## Create a conda env and install mxnet
```
conda create -n keras_mxnet —clone root
pip install mxnet-cu80==0.11.0

# check installed version
$  python -c "import mxnet; print(mxnet.__version__)"
0.11.0
```

## Install Keras
```
export PYTHON_PATH=~/anaconda2/envs/keras_mxnet/
git clone https://github.com/dmlc/keras.git
cd keras
python setup.py install
```

then you need to activate the mxnet backend
```
export KERAS_BACKEND=mxnet

$ python -c "import keras; print(keras.__version__)"
Using MXNet backend.
1.2.2
```

## Using GPUs
You just need to provide device names in `context` variable of your model
```
model.compile(loss='categorical_crossentropy',
              optimizer=SGD(),
              metrics=['accuracy'],
              context=['gpu(0)','gpu(1)'])
```

### Benchmark testing
This [repo](https://github.com/sandeep-krishnamurthy/keras-mxnet-benchmarks) provides Keras examples for profiling performance.

Here is what I do in conda env
```
conda install cudnn cudatoolkit
export CUDA_HOME=/usr/local/cuda-8.0
export PATH=$CUDA_HOME/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64/:$LD_LIBRARY_PATH

pip install nose
pip install nose-parameterized
pip install memory_profiler
```

Here is a benchmark test result, conducted on washington with 2 GPUs (12GB each)

| profile                               | Tensorflow |  MXNet | MXNet (w/ batch size 100x) |
| --------------------------------------|-----------:|-------:|---------------------------:|
| Number of images processed per second | 559.35     | 1076.69| 4610.49                    |
| Maximum total memory consumption      | 23833.0    | 2152.0 | 19488.0                    |
| Training Time (in secs)               | 1072.67    | 557.26 | 130.14                     |



