# Recreates SpliceBERT Results and Runs Small Scale SimCSP

## TODO: 
- implement compare.py
- implement pretrain_MLM.py 
    - integrate into pretrain.sh and finetune.sh

## EXPERIMENTS: 
- 1: relationship between f1/sccs in pretrain and fine-tune and its affects on F1 score 
    - uses the last layer's [CLS] token 
    - uses SpliceBERT-human, evaluated using f1/sccs on spliceator and NMI on hg19
    - could be improved by using SpliceBERT and NMI on spliceator 
- 2: experiment with chopping off k layers and doing CL + fine-tune on that

## METRICS:
- SCCS : spearman correlation w/ cosine similarity 
- NMI : normalized mutual information 
- F1 : linear combination of precision and recall

## COMPUTE QUEUE:
Exp1: 
- exp1 finetune
Exp2 (5_hidden): 
- exp2 pretrain
- exp2 finetune 
Exp2 (4_hidden): 
- exp2 pretrain
- exp2 finetune 
Exp2 (3_hidden): 
- exp2 pretrain
- exp2 finetune 

## NOTES: 
- cite UMAP and leiden algorithm + give more explanation on generation
- hrg uses hg38 and umap plotting uses hg19 but K562 uses hg38 so can only be used w/ msg
    - if pre-training on msg then should use spliceator test set for NMI evaluation
- spliceator num_samples 44,152
- until SpliceBERT-human MLM is implemented correctly, might be learning from hrg during CL 

## EXPERIMENTAL PIPELINE:
- pretrain.sh
- finetune.sh

## KNOWN IMPROVEMENTS: 
- bigger model
- more diverse training data
- use middle transformer layers 
- use mean pooling across some linear combination of hidden layers 

## IDEAS: 
- experiment with training the classification head with frozen transformer layers first
- use a splice site location tool to generate a better MLM training set (or microsoft paper idea)
- use a MLM and CL loss function together during pre-train
- explore Sup. CL
