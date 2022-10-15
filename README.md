<div>
# Build Gradio inference app

## Step1:
Train Model on Colab for 10 epochs and download scripted model model.script.pt and create a tar.gz file named model.script.pt.tar.gz

## Step2:
Build docker image using command below (inference code is in src/demo.py):

docker build -t timm-gradio-cifar10

## Step3:
Start gradio app by running docker image at port 8080

docker run -p 8080:7860 timm-gradio-cifar10

## Step4:
Push the docker image to dockerhub

docker login
docker image tag timm-gradio-cifar10 monimoyp/timm-gradio-cifar10:latest
ocker image push monimoyp/timm-gradio-cifar10:latest




# Train on Docker and Predict on cog using Pytorch ligtning and Hydra Template

This repository is created using template from https://github.com/ashleve/lightning-hydra-template.<br>

Building of Docker images and downloading of cog binary is by building Makefile. CIFAR10 images are trained on Docker using Pytorch lighning, timm and hydra template.
  
Prediction on any image is done using cog by integrating timm.

</div>

<br>

## 📌 How to Use

**How to build:**

make build

**How to train:** 

docker run -v \`pwd\`:/workspace/project cifar10_emlo python3 src/train.py experiment=cifar

**How to predict using cog:**

make predict image=\<Image File\>

Example:
make predict image=input.jpg

**How to tune parameters of cifar10 using resnet**

python3 src/train.py -m experiment=cifar hparams_search=cifar10_optuna

<br>



## Project Structure

The directory structure of new project looks like this:

```
├── configs                   <- Hydra configuration files
│   ├── callbacks                <- Callbacks configs
│   ├── datamodule               <- Datamodule configs
│   ├── debug                    <- Debugging configs
│   ├── experiment               <- Experiment configs
│   ├── extras                   <- Extra utilities configs
│   ├── hparams_search           <- Hyperparameter search configs
│   ├── hydra                    <- Hydra configs
│   ├── local                    <- Local configs
│   ├── logger                   <- Logger configs
│   ├── model                    <- Model configs
│   ├── paths                    <- Project paths configs
│   ├── trainer                  <- Trainer configs
│   │
│   ├── eval.yaml             <- Main config for evaluation
│   └── train.yaml            <- Main config for training
│
├── data                   <- Project data
│
├── logs                   <- Logs generated by hydra and lightning loggers
│
├── notebooks              <- Jupyter notebooks. Naming convention is a number (for ordering),
│                             the creator's initials, and a short `-` delimited description,
│                             e.g. `1.0-jqp-initial-data-exploration.ipynb`.
│
├── scripts                <- Shell scripts
│
├── src                    <- Source code
│   ├── datamodules              <- Lightning datamodules
│   ├── models                   <- Lightning models
│   ├── utils                    <- Utility scripts
│   │
│   ├── eval.py                  <- Run evaluation
│   └── train.py                 <- Run training
│
├── tests                  <- Tests of any kind
│
├── .env.example              <- Example of file for storing private environment variables
├── .gitignore                <- List of files ignored by git
├── .pre-commit-config.yaml   <- Configuration of pre-commit hooks for code formatting
├── Makefile                  <- Makefile with commands like `make train` or `make test`
├── pyproject.toml            <- Configuration options for testing and linting
├── requirements.txt          <- File for installing python dependencies
├── setup.py                  <- File for installing project as a package
└── README.md
```

<br>

