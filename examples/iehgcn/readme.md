# Interpretable and Efficient Heterogeneous Graph Convolutional Network (ieHGCN)

- Paper link: [https://arxiv.org/abs/2005.13183v3](https://arxiv.org/abs/2005.13183v3)
- Author's code repo: [https://github.com/kepsail/ie-HGCN](https://github.com/kepsail/ie-HGCN). Note that the original code is 
  implemented with Pytorch for the paper.

# Dataset Statics

| Dataset | # Nodes | # Node Types | # Edges | # Edge Types | Target | # Classes |
| ------- | ------- |--------------| ------- | ------------ | ------ |-----------|
| DBLP    | 26,128  | 4            | 239,566 | 6            | author | 4         |
| IMDB    | 21,420  | 4            | 86,642  | 6            | movie  | 4         |

DBLP dataset refer to [HGBDataset](https://gammagl.readthedocs.io/en/latest/api/gammagl.datasets.html#gammagl.datasets.HGBDataset).

IMDBdataset refer to [IMDB](https://gammagl.readthedocs.io/en/latest/api/gammagl.datasets.html#gammagl.datasets.IMDB).

# Performance
> For the DBLP dataset: train test val = 974, 1420, 243 about  37% for training.
> 
> For the IMDB dataset: train test val = 400, 3478, 400, about 9% for training.

| Dataset | Paper(80% training) | Paper(60% training) | Paper(40% training) | Paper(20% training) | Our(tf)     | Our(th)     | Our(pd)     |
|---------|---------------------|---------------------|---------------------|---------------------|-------------|-------------|-------------|
| IMDB    | 58.35               | 60.84               | 59.81               | 56.60               | 57.23±0.83% | 55.22±1.21% | 56.08±2.13% |

```bash
TL_BACKEND="torch" python3 iehgcn_trainer.py --dataset IMDB --n_epoch 100 --lr 0.005 --num_layers 3 --hidden_channels [64, 32] --l2_coef 0.0005 --drop_rate 0.2
TL_BACKEND="tensorflow" python3 iehgcn_trainer.py --dataset IMDB --n_epoch 25 --lr 0.005 --num_layers 3 --hidden_channels [64, 32] --l2_coef 0.0005 --drop_rate 0.2
TL_BACKEND="paddle" python3 iehgcn_trainer.py --dataset IMDB --n_epoch 25 --lr 0.005 --num_layers 3 --hidden_channels [64, 32] --l2_coef 0.0005 --drop_rate 0.2
```