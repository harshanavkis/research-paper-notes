# DFTS: Deep Feature Transmission Simulator

## Environment setup(for windows)

* The requirements.txt file can be found in the same directory as the source code

### Without Conda

```
python -m venv dftsEnv
dftsEnv\Scripts\activate
pip install -r requirements.txt
```

### Conda

```
conda create -n dftsEnv
activate dftsEnv
pip install -r requirements.txt
```

## Configuration File:

Navigate to the folder containing the source code and open params.yml:
* Task: objective of the model
  * (value=0): Classification
  * epochs: number of simulations
* TestDir:
  * top directory containing the images
    * for classification the images must be stored in a folder whose name is the class number(imagenet like)
* Preprocess:
  * reshapeDims: enter the reshape dimensions as a python list
  * batch_size : number of images to be forwarded at a time through a network
  * normalize  : set to a boolean value, True or False
* Model:
  * kerasmodel: enter an official model or a link to the model(not tested currently, so might not work)
* SplitLayer:
  * split: enter the layer at which the model needs to be split. The name should be entered exactly as it was named during creation. Layer names can be accessed by getting the output of model.summary(), where model is the keras model.
* Transmission:
  * rowsperpacket: number of rows of the feature map per packet, must be integer
  * quantization : enter number of bits and a bool(True or False) to include it
  * channel      : enter True for a particular channel that you wish to select, and set its parameters. If more than one channel is set True, program exits. If all are False no channel is used in the simulation.
  * concealment  : enter True for the concealment you wish to select and set its parameters, if any. If more than one concealment is set True, program exits. If all are False no channel is selected.
* OutputDir: location of the directory where the test data must be stored
  
## Running your own simulations:
Change your current working directory to the source directory containing main.py .

```
python main.py -p params.yml
```

Keep an eye on the terminal for interesting stats!!
