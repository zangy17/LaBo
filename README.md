# LaBo
Code for the paper "Language in a Bottle: Language Model Guided Concept Bottlenecks for Interpretable Image Classification"

## Set up environments
We run our experiments using Python 3.9.13. You can install the required packages using:

```
pip install -r requirements.txt
```

## Directories
* `cfg/` saves the config files for all experiments including both linear probe (`cfg/linear_probe`) and LaBo (`cfg/asso_opt`). You can modify the config files to change the arguments of the system.
* `datasets/` stores the dataset-specific data including `images`, `splits`, `concepts`. Please check `datasets/DATASET.md` for details. 

	**Note**: the images of each dataset are not provided in this repo, you need to download them and 	store in the corresponding folder: `datasets/{dataset name}/images/`.
	
* `exp/` is the work directories of the experiments, the config files and model checkpoints will be saved in this folder.
* `models/` saves the models:
	* Linear Probe: `models/linear_prob/linear_prob.py`
	* LaBo: `models/asso_opt/asso_opt.py`
	* concept selection functions: `models/select_concept/select_algo.py`
* `output/`: the performance will be saved into `.txt` files stored in `output/`.
* Other files: 
	* `data.py` and `data_lp.py` are the dataloader for LaBo and Linear Probe, respectively.
	* `main.py` is the interface to run all experiments and `utils.py` contains the preprocess and feature extraction functions.
	* `linear probe.sh` is the bash file to run linear probe. `labo_train.sh` and a`labo_test.sh` are the bash file to train and test LaBo.

## Linear Probe
To get the linear probe performance, just run:

```
sh linear_probe.sh {DATASET} {SHOTS} {CLIP SIZE}
```
For example, for flower dataset 1-shot with ViT-L/14 image encoder, the command is:

```
sh linear_probe.sh flower 1 ViT-L/14
```

The code will automatically encoder the images and run hyperparameter search on the L2 regularization using the dev set. The best validation performance and the test performance will be saved in the `output/linear_probe/{DATASET}.txt`.

## LaBo Training
To train the LaBo, run the following command:

```
sh labo_train.sh
```

## Testing
