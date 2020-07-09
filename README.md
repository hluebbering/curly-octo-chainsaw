Caliban Tutorial
================

## What is Caliban?

### Caliban is

    - a tool to launch and track numerical experiments in a computing environment
    
    - go from a prototype to thousands of experimental jobs running on the Cloud
    
    - developed by machine learning researchers and engineers

### Train a neural network on the local machine

  - train an image classification network (implemented in TensorFlow)

  - increase model’s accuracy by changing the learning rate

  - sweep across a range of learning rates

  - train the model in the cloud on Google’s AI Platform

  - develop code using caliban shell

## Installation

### 1\. In terminal:

```{bash}
pip install caliban
```

### 2\. Get docker:

<https://hub.docker.com/editions/community/docker-ce-desktop-mac>

### 3\. Set up google cloud account:

<https://caliban.readthedocs.io/en/latest/getting_started/cloud.html>

### 4\. Install google cloud SDK in terminal:

``` {bash}
./google-cloud-sdk/install.sh

gcloud init
```

### 5\. Create Enviroment Variables:

1.  set up **.zshrc** (or .bash\_profile)

<!-- end list -->

``` {bash}
nano.zshrc
```

2.  add following variables:

<!-- end list -->

``` {bash}
./google-cloud-sdk/install.sh

export PROJECT_ID=<your-project-id>

export GOOGLE_APPLICATION_CREDENTIALS=$HOME/.config/service_key.json
```

## Training Neural Networks

### 1\. Setup:

``` {bash}
mkdir demo && cd demo

curl --output mnist.py https://raw.githubusercontent.com/google/caliban/master/tutorials/basic/mnist.py

echo "tensorflow-cpu" > requirements.txt
```

### 2\. Train a basic neural network

``` {bash}
caliban run --nogpu mnist.py
```

*Training model with learning rate=0.1 for 3 epochs* *accuracy: 0.2328*

### 3\. Improve Model:

``` {bash}
caliban run --nogpu mnist.py -- --learning_rate 0.01
```

*accuracy: 0.9549\!\!\!*

### 4\. Experiment Brodcasting:

1.  create a .json file in terminal

<!-- end list -->

``` {bash}
echo '{"learning_rate": [0.01, 0.001, 0.0001]}' > experiment.json`
```

2.  run following command with configuration in **terminal**

<!-- end list -->

``` {bash}
caliban run --experiment_config experiment.json --nogpu mnist.py
```

### 5\. Submitting to Cloud AI Platform:

``` {bash}
gcloud config set project prickly-cactus

caliban cloud --nogpu mnist.py -- --learning_rate 0.01
```

    what caliban is doing:
    
    - building a Docker container with all of your code
    
    - moving that container to google cloud's container registry
    
    - submitting the job to AI Platform

-----

<div id="refs" class="references hanging-indent">

<div id="ref-caliban2020github">

Ritchie, Sam, Ambrose Slone, and Vinay Ramasesh. 2020. *Caliban:
Docker-Based Job Manager for Reproducible Workflows* (version 0.2.5).
<http://github.com/google/caliban>.

</div>

</div>
