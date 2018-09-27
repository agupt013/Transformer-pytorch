# Transformer-pytorch
A PyTorch implementation of Transformer in "Attention is All You Need" (https://arxiv.org/abs/1706.03762)

This repo focuses on clean, readable, and modular implementation of the model.

<img width="559" alt="screen shot 2018-09-27 at 1 49 14 pm" src="https://user-images.githubusercontent.com/2340721/46123973-44b08900-c25c-11e8-9468-7aef9e4e3f18.png">

## Requirements
- Python 3.6+
- [PyTorch 4.1+](http://pytorch.org/)
- [NumPy](http://www.numpy.org/)
- [NLTK](https://www.nltk.org/)
- [tqdm](https://github.com/tqdm/tqdm)

## Usage

### Prepare datasets
This repo comes with example data in `data/` directory. To begin, you will need to prepare datasets with given data as follows:
```
$ python prepare_datasets.py --train_source=data/raw/src-train.txt --train_target=tgt-train.txt --val_source=src-val.txt --val_target=tgt-val.txt --save_data=data/processed
```

The example data is brought from [OpenNMT-py](https://github.com/OpenNMT/OpenNMT-py).
The data consists of parallel source (src) and target (tgt) data for training and validation.
A data file contains one sentence per line with tokens separated by a space.
Below are the provided example data files.

- `src-train.txt`
- `tgt-train.txt`
- `src-val.txt`
- `tgt-val.txt`

### Train model
To train model, provide the train script with a path to processed data and save files as follows:

```
$ python train.py --data=data/example/processed --save_config=checkpoints/example_config.json --save_checkpoint=checkpoints/example_model.pth 
```

You can play around with hyperparameters of the model with command line arguments. 
For example, add `--layers_count=4` to set the number of layers as 5. 

### Translate
To translate a sentence in source language to target language:
```
$ python predict.py --source="There is an imbalance here ." --config=checkpoints/example_config.json --checkpoint=checkpoints/example_model.pth

Candidate 1 : Hier fehlt das Gleichgewicht .
Candidate 2 : Hier fehlt das .
Candidate 3 : Hier fehlt .
```

It will give you translation candidates of the given source sentence.
You can adjust the number of candidates with command line argument. 

### Evaluate
To calculate BLEU score of a trained model:
```
$ python evaluate.py --save_result=logs/example_eval.txt --config=checkpoints/example_config.json --checkpoint=checkpoints/example_model.pth

BLEU score : 10.0
```

## File description
- `models.py` includes Transformer's encoder, decoder, and multi-head attention.
- `embeddings.py` contains positional encoding.
- `losses.py` contains label smoothing loss.
- `optimizers.py` contains Noam optimizer.
- `metrics.py` contains accuracy metric.
- `beam.py` contains beam search.
- `datasets.py` has code for loading and processing data. 
- `trainer.py` has code for training model.
- `prepare_datasets.py` processes data.
- `train.py` trains model.
- `predict.py` translates given source sentence with a trained model.
- `evaluate.py` calculates BLEU score of a trained model.

## Reference
- [OpenNMT-py](https://github.com/OpenNMT/OpenNMT-py)

## Author
[@dreamgonfly](https://github.com/dreamgonfly)