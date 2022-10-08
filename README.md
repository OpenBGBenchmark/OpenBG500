## OpenBG500

### Information

**OpenBG500** is an open chinese E-commerce and bussiness knowledge graph dataset contained 500 relations. This dataset is refined from the [OpenBG](https://kg.alibaba.com/), a million-scale multi-modal dataset evolving products and consumption demands in a unified schema. AliOpenKG500 is developed for several knowledge graph embedding evaluations.

The dataset splits all data into 3 parts. Base statistical information is shown in the table below.

| #Relation | #Entity | #Train (opened) | #Valid (opened) | #Test  |
| :-------: | :-----: | :-------------: | :-------------: | :----: |
|    500    | 249,743  |     1242550     |     5000      | 5000 |

### Data

OpenBG500 is available at [Google Drive](https://drive.google.com/file/d/1pD_icqV-lLbCXN2rfBaq-Y5i_XcKVCzM/view?usp=sharing) and [Baidu Netdisk(password: 78fw)](https://pan.baidu.com/s/1NsRWct-u63QmxVgyjJeXsg). The main derectory of the dataset is as follows.

```
OpenBG500
├── OpenBG500_train.tsv 			# Training set
├── OpenBG500_dev.tsv 				# Validation set
├── OpenBG500_test.tsv 			    # Test set
├── OpenBG500_entity2text.tsv 		# Description of entities in Chinese
├── OpenBG500_relation2text.tsv 	# Description of relations in Chinese
└── OpenBG500_example_pred.tsv 	    # Submit example
```

### Usage

#### Format

* Triples

```shell
# {Dataset}_train.tsv/{Dataset}_dev.tsv
Head<\t>Relation<\t>Tail<\n>
```

* Description of entities/relations in Chinese

```shell
# {Dataset}_entity2text.tsv/{Dataset}_relation2text.tsv
Entity(Relation)<\t>Description of entitie(relation)<\n>
```

* Test and submit

```shell
# For {Dataset}_test.tsv, participants are required to predict 10 Tails for one instance. {Dataset}_example_pred.tsv is a submit example.
Head<\t>Relation<\n>

# {Dataset}_example_pred.tsv
Head<\t>Relation<\t>Tail 1<\t>Tail 2<\t>...<\t>Tail 10<\n>
```

#### Check the data

```
$ head -n 3 {Dataset}_train.tsv
ent_135492      rel_0352        ent_015651
ent_020765      rel_0448        ent_214183
ent_106905      rel_0418        ent_121073
```

#### Read the datasets

1. Read the original data:
```python
with open('{Dataset}_train.tsv', 'r') as fp:
    data = fp.readlines()
    train = [line.strip('\n').split('\t') for line in data]
    _ = [print(line) for line in train[:2]]
    # ['ent_135492', 'rel_0352', 'ent_015651']
    # ['ent_020765', 'rel_0448', 'ent_214183']
```

2. Get the map of Entity(Relatioin)-Description: `ent2text` and `rel2text`:
```python
with open('{Dataset}_entity2text.tsv', 'r') as fp:
    data = fp.readlines()
    lines = [line.strip('\n').split('\t') for line in data]
    _ = [print(line) for line in lines[:2]]
    # ['ent_101705', '短袖T恤']
    # ['ent_116070', '套装']

ent2text = {line[0]: line[1] for line in lines}

with open('{Dataset}_relation2text.tsv', 'r') as fp:
    data = fp.readlines()
    lines = [line.strip().split('\t') for line in data]
    _ = [print(line) for line in lines[:2]]
    # ['rel_0418', '细分市场']
    # ['rel_0290', '关联场景']

rel2text = {line[0]: line[1] for line in lines}
```

3. Transfer the data to description: 
```python
train = [[ent2text[line[0]],rel2text[line[1]],ent2text[line[2]]] for line in train]
_ = [print(line) for line in train[:2]]
# ['苦荞茶', '外部材质', '苦荞麦']
# ['精品三姐妹硬糕', '口味', '原味硬糕850克【10包40块糕】']
```

### Submit in Alibaba TIANCHI

[OpenBG Benchmark：Large Scale Open Business Knowledge Graph Benchmark](https://tianchi.aliyun.com/dataset/dataDetail?dataId=122271) is a benchmark open for a long time. Welcome to submit your result of OpenBG500.

### Baseline result

We do some baseline method on this dataset. `TransE`, `DistMult` and `ComplEx` result are based on `OpenKE` toolkit, `KG-BERT` and `GenKGC` results are based our code.
| Method   | Hits@1 | Hits@3 | Hits@10 |
| -------- | ------ | ------ | ------- |
| TransE   | 0.207  | 0.340  | 0.531   |
| DistMult | 0.049  | 0.088  | 0.216   |
| ComplEx  | 0.053  | 0.120  | 0.266   |
| KG-BERT  | 0.023  | 0.049  | 0.241   |
| [GenKGC](https://arxiv.org/abs/2202.02113)   | 0.203  | 0.280  | 0.351   |


