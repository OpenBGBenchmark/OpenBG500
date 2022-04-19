## OpenBG500

### Information

**OpenBG500** is an open chinese E-commerce and bussiness knowledge graph dataset contained 500 relations. This dataset is refined from the [AliOpenKG](https://kg.alibaba.com/), a million-scale multi-modal dataset evolving products and consumption demands in a unified schema. AliOpenKG500 is developed for several knowledge graph embedding evaluations.

The dataset splits all data into 3 parts. Base statistical information is shown in the table below.

| #Relation | #Entity | #Train (opened) | #Valid (opened) | #Test  |
| :-------: | :-----: | :-------------: | :-------------: | :----: |
|    500    | 269658  |     1242550     |     5000      | 5000 |

### Data

OpenBG500 is available at [Google Drive](https://drive.google.com/drive/folders/1QgSL1wcLmA_eOQibwKxDaxVRGrMFqDMV?usp=sharing). The dataset offers two triplet formats for convenient evaluations and the main derectory of the dataset is as follows.

```
.	              # Format 1: 
├── entity2id.txt         # Entities to ids
├── entityid_map.txt        # Entity ids to labels in chinese
├── relation2id.txt       # Relations to ids
├── relationid_map.txt      # Relation ids to lables in chinese
├── train2id.txt          # Triplets in train set to ids
├── valid2id.txt          # Triplets in valid set to ids
├── other_format          # Format 2: 
│   ├── entity_map.txt      # Raw entities to labels in chinese
│   ├── relation_map.txt    # Raw relations to labels in chinese
│   ├── train             # Triplets in train set
└── └── valid             # Triplets in valid set
```

### Format

**Format 1** follows style of datasets in [OpenKE](https://github.com/thunlp/OpenKE). 

```
# train2id.txt
1242550					# Number of triplets in file
head_entity_id <tab> tail_entity_id <tab> relation_id <\n>
...

# entity2id.txt
269658					# Number of entities in file
raw_entity_name <tab> entity_id <\n>
...

# entityid_map.txt
entity_id <tab> entity_label_ch <\n>
...
```

**Format 2** follows original style in AliOpenKG. 

```
# train
raw_head_entity_name <tab> raw_relation_name <tab> raw_tail_entity_name <\n>
...

# entity_map.txt
raw_entity_name <tab> entity_label_ch <\n>
...
```


