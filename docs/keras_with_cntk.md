# Using Keras with CNTK backend

CNTK is a deep learning toolkit developed by [Microsoft](https://docs.microsoft.com/en-us/cognitive-toolkit/).
This document is based on CNTK 2.2

## Create a conda env and install CNTK

```
conda create -n keras_cntk —clone root
source activate keras_cntk
conda install opencv
pip install https://cntk.ai/PythonWheel/GPU/cntk-2.2-cp27-cp27mu-linux_x86_64.whl
export LD_LIBRARY_PATH=~/anaconda2/envs/keras_cntk/lib/

$ python -c "import cntk; print(cntk.__version__)"
2.2
```

## Install Keras and configure env variable to activate CNTK
```
conda install keras
export KERAS_BACKEND=cntk
```
