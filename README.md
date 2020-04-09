# GNN-TabFact
This is the state-of-the-art models on [TabFact Dataset](https://tabfact.github.io/), we leverage the idea proposed in [NumGNN](https://arxiv.org/pdf/1910.06701.pdf) into the encoding of tabular data.


# Requirements:
- [HuggingFace Transformers](https://github.com/huggingface/transformers)
- tensorboardX
- pandas


# Architecture
- Cross-Attention Between Table and Statement to obtain the representation
- Construct the greater/less mask for the table numeric columns
- Use the the dense greater/less connection to propagate the information in each cell
- Obtain the graph repsentation obtained by the NumGNN
- Finally use it to do the two-way classification.


# Performance
We demonstrate our results as follows:
| Model     | Dev  | Test |
|-----------|------|------|
| TableBERT | 66.1 | 65.1 |
| GNN       | 72.1 | 72.2 |


# Training and Evaluating
Creating a folder for saving the model
```
mkdir models
```

Downloading the pre-trained model from Amazon S3
```
cd models
wget 
```

Loading the trained GNN Model and reproduce the results:
```
CUDA_VISIBLE_DEVIES=0 python gnn.py --model bert-base-multilingual-uncased --do_test --encoding gnn --load_from models/gnn_fp16_numeric/model_ep4.pt
```

Retrain your own GNN Model for TabFact:
```
CUDA_VISIBLE_DEVIES=0 python gnn.py --model bert-base-multilingual-uncased --do_train --encoding gnn --output_dir models/gnn_fp16_numeric_test --attention cross --lr_default 5e-6
```



