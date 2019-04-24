# Natural Language Understanding with Computational Semantics

## Visual Commonsense Reasoning

Members:
  - Mihir Rana
  - Kenil Tanna

Advisors:
  - Kyunghyun Cho
  - Samuel R. Bowman

## Setting up and using the repo

1. Get the dataset. Follow the steps in `data/README.md`. This includes the steps to get the pretrained BERT embeddings.

2. Install cuda 9.0 if it's not available already. You might want to follow this [this guide](https://medium.com/@zhanwenchen/install-cuda-9-2-and-cudnn-7-1-for-tensorflow-pytorch-gpu-on-ubuntu-16-04-1822ab4b2421) but using cuda 9.0. I use the following commands (my OS is ubuntu 18.04):
```
wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda_9.0.176_384.81_linux-run
chmod +x cuda_9.0.176_384.81_linux-run
./cuda_9.0.176_384.81_linux-run --extract=$HOME
sudo ./cuda-linux.9.0.176-22781540.run
sudo ln -s /usr/local/cuda-9.0/ /usr/local/cuda
export LD_LIBRARY_PATH=/usr/local/cuda-9.0/
```

3. Install anaconda if it's not available already, and create a new environment. You need to install a few things, namely, pytorch 1.0, torchvision (*from the layers branch, which has ROI pooling*), and allennlp.

```
wget https://repo.anaconda.com/archive/Anaconda3-5.2.0-Linux-x86_64.sh
conda update -n base -c defaults conda
conda create --name vcr python=3.6
source activate vcr

conda install numpy pyyaml setuptools cmake cffi tqdm pyyaml scipy ipython mkl mkl-include cython typing h5py pandas nltk spacy numpydoc scikit-learn jpeg

conda install pytorch cudatoolkit=9.0 -c pytorch
pip install git+git://github.com/pytorch/vision.git@24577864e92b72f7066e1ed16e978e873e19d13d

pip install -r allennlp-requirements.txt
pip install --no-deps allennlp==0.8.0
python -m spacy download en_core_web_sm


# this one is optional but it should help make things faster
pip uninstall pillow && CC="cc -mavx2" pip install -U --force-reinstall pillow-simd
```

4. If you don't want to download from scratch, then download my checkpoint.

```
wget https://s3-us-west-2.amazonaws.com/ai2-rowanz/r2c/flagship_answer/best.th -P models/saves/flagship_answer/
wget https://s3-us-west-2.amazonaws.com/ai2-rowanz/r2c/flagship_rationale/best.th -P models/saves/flagship_rationale/
```

5. That's it! Now to set up the environment, run `source activate vcr && export PYTHONPATH=$HOME/visual_commonsense_reasoning/` (or wherever you have this directory).