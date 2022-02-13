## envs

```
pip install -r requirements.txt
```

## download dataset

* for reddit and ogbn-products: come with dgl/ogb packages
    * reddit: `dgl.data.RedditDataset(raw_dir=ROOT_PATH, self_loop=True)`
    * ogbn-products: `ogb.nodeproppred.DglNodePropPredDataset(root=ROOT_PATH, name='ogbn-products')`
* for yelp and amazon: download from [GraphSAINT repo](https://github.com/GraphSAINT/GraphSAINT)

we denote the root directory that contains dataset as <ROOT_PATH>

## reproduce 

for the vanilla MOS-GCN:
```
CUDA_VISIBLE_DEVICES=0 python train.py --root <ROOT_PATH> --n-hidden 128 --dataset reddit --lr 0.01 --dropout 0.2 --node-budget 8000 --n-epochs 40 --val-every 1
CUDA_VISIBLE_DEVICES=0 python train.py --root <ROOT_PATH> --n-hidden 512 --dataset yelp --lr 0.1 --dropout 0.1 --node-budget 29000 --n-epochs 90 --val-every 1
CUDA_VISIBLE_DEVICES=0 python train.py --root <ROOT_PATH> --n-hidden 512 --dataset ogbn-products --lr 0.001 --dropout 0.3 --node-budget 36000 --n-epochs 200 --val-every 10
CUDA_VISIBLE_DEVICES=0 python train.py --root <ROOT_PATH> --n-hidden 512 --dataset amazon --lr 0.1 --dropout 0.1 --node-budget 31000 --n-epochs 40 --val-every 1
```

for the decomposed MOS-GCN:
```
CUDA_VISIBLE_DEVICES=0 python train.py --root <ROOT_PATH> --n-hidden 128 --dataset reddit --lr 0.01 --dropout 0.2 --node-budget 9000 --decomp 4 --n-epochs 40 --val-every 1
CUDA_VISIBLE_DEVICES=0 python train.py --root <ROOT_PATH> --n-hidden 512 --dataset yelp --lr 0.1 --dropout 0.1 --node-budget 29000 --decomp 8 --n-epochs 90 --val-every 1
CUDA_VISIBLE_DEVICES=0 python train.py --root <ROOT_PATH> --n-hidden 512 --dataset ogbn-products --lr 0.001 --dropout 0.3 --node-budget 36000 --decomp 4 --n-epochs 200 --val-every 10
CUDA_VISIBLE_DEVICES=0 python train.py --root <ROOT_PATH> --n-hidden 512 --dataset amazon --lr 0.1 --dropout 0.1 --node-budget 40000 --decomp 4 --n-epochs 40 --val-every 1
```

