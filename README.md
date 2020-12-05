
CIKM 2020 ["**S3-Rec: Self-Supervised Learning for Sequential
 Recommendation with Mutual Information Maximization"**](https://arxiv.org/pdf/2008.07873.pdf)

## Overview
![avatar](model.PNG)

## Reproduce
Please check the ./reproduce/ directory.

## Results

**99 negative sample version**. The used test files are name as 
```
data-name_sample.txt
```
![avatar](sample_99.PNG)


**all the items version** .
We omit the FM and AutoInt because they need 
enumerate all user-item pairs, which take a very long time. 

![avatar](all_rank.PNG)


## data format
- data preprocess
```shell script
./data/data_process.py
```


- generate negative items for testing
```shell script
./data/generate_test.py
```

- data format
```shell script
data-name.txt
user_1 item_1 item_2 ...
user_2 item_1 item_2 ...

data-name_sample.txt
user_1 neg_item_1 neg_item_2 ...
user_2 neg_item_1 neg_item_2 ...

data-name_item2attributes.json
{item_1:[attr, ...], item_2:[attr, ...], ... }
```

## pretrain
```shell script
python run_pretrain.py --data_name data_name
```

## finetune
Check the ./reproduce directory.

+ Rank ground-truth item with 99 randomly sampled negative items
```shell script
python run_finetune_sample.py \
--data_name data_name \
--ckp pretrain_epochs_num
```

+ Rank the ground-truth item with all the items
```shell script
python run_finetune_full.py \
--data_name data_name \
--ckp pretrain_epochs_num
```
