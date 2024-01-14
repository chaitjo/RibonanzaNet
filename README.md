# RibonanzaNet

Training code for RibonanzaNet

## Data Download

You just need ```train_data.csv``` and ```test_sequences.csv``` from 
https://www.kaggle.com/competitions/stanford-ribonanza-rna-folding/data

## Environment

Create the environment from the environment file ```env.yml```

```conda env create -f env.yml```

Install ranger optimizer

```
git clone https://github.com/lessw2020/Ranger-Deep-Learning-Optimizer
cd Ranger-Deep-Learning-Optimizer
pip install -e .
``` 

## How to run

### Training
```accelerate launch run.py --config_path configs/pairwise.yaml```

### Inference
```accelerate launch inference.py --config_path configs/pairwise.yaml```

### Process raw prediction into submission file for Ribonanza
```python make_submission.py --config_path configs/pairwise.yaml```


## Configuration File

This section explains the various parameters and settings in the configuration file for RibonanzaNet

### Model Hyperparameters
- `learning_rate`: 0.001  
  The learning rate for the optimizer. Determines the step size at each iteration while moving toward a minimum of the loss function.

- `batch_size`: 2  
  Number of samples processed per GPU per batch. 

- `test_batch_size`: 8  
  Batch size used for testing the model.

- `epochs`: 40  
  Total number of training cycles the model goes through.

- `dropout`: 0.05  
  The dropout rate for regularization to prevent overfitting. It represents the proportion of neurons that are randomly dropped out of the neural network during training.

- `weight_decay`: 0.0001  
  Regularization technique to prevent overfitting by penalizing large weights.

- `k`: 5
  1D Convolution kernel size

- `ninp`: 256  
  The size of the input dimension.

- `nlayers`: 9  
  Number of RibonanzaNet blocks.

- `nclass`: 2  
  Number of classes for classification tasks.

- `ntoken`: 5  
  Number of tokens (AUGC + padding/N token) used in the model.

- `nhead`: 8  
  The number of heads in multi-head attention models.

- `use_flip_aug`: true  
  Indicates whether flip augmentation is used during training/inference.

- `gradient_accumulation_steps`: 2  
  Number of steps to accumulate gradients before performing a backward/update pass.

- `use_triangular_attention`: false  
  Specifies whether to use triangular attention mechanisms in the model.

- `pairwise_dimension`: 64  
  Dimension of pairwise interactions in the model.

### Data Scaling
- `use_data_percentage`: 1  
  The percentage of data used from the dataset.

- `use_dirty_data`: true  
  Indicates whether to include 'dirty' or noisy data in the training process. Useful for testing robustness or when clean data is limited.

### Other Configurations
- `fold`: 0  
  The current fold in use if the data is split into folds for cross-validation.

- `nfolds`: 6  
  Total number of folds for cross-validation.

- `input_dir`: "../../input/"  
  Directory for input data. Put ```train_data.csv``` and ```test_sequences.csv``` here. 

- `gpu_id`: "0"  
  Identifier for the GPU used for training. Useful in single-GPU setup.

---

## File structure
 
```logs``` has the csv log file with train/val oss,
```models``` has model weights and optimizer states,
```oofs``` has the val predictions



