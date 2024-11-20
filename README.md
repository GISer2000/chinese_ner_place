## 简介
嵌入在线自然语言文本中的地名是地理信息的有用来源。尽管如此，许多从文本中提取地名的方法都使用未专门为此任务设计的预训练模型。本项目参考《[Transformer based named entity recognition for place name extraction from unstructured text](https://doi.org/10.1080/13658816.2022.2133125)》的方法，使用中文数据集，训练了一个用于从中文非结构化的文本中提取地名。

文件说明：
- data：文本，包括标注数据
- bert_ner.ipynb：基线模型
- bert_crf_ner.ipynb：拟议模型
- crf.py：条件随机场（Conditional Random Field），拟议模型需要用到
- model/bert-base-chinese：需要自己下载[Bert](https://huggingface.co/google-bert/bert-base-chinese)模型，放到这个目录（没有的话自己创建）

## 标注数据
使用[MarkStudio](https://github.com/cuiwang/MarkStudio)进行实体标注。MarkStudio是一款功能丰富的数据标注工具，已支持`实体标注`、`文本分类`、`文本翻译`、`关系标注`、`对话标注`。

使用`BIO-三位序列标注法`(B-begin，I-inside，O-outside)标注数据：
- B-X代表实体X的开头
- I-X代表实体X的中间或结尾
- O代表不属于任何类型的

## 拟议模型
- Embedding layer：
  - Pre-trained: Transformer
- Intermediate layers:
  - Transformer
- Classification layer:
  - CRF
 
## 结果
数据集说明
- 500条标注数据
- 数据划分：train:val:test ——> 8:1:1

测试集上的精度：
| **模型**      | **Accuracy** | **Macro-Precision** | **Macro-Recall** | **Macro-F1** |
|---------------|--------------|---------------------|------------------|--------------|
| **BERT**      | 0.9962       | 0.9822                | 0.9880         | 0.9851       |
| **BERT_CRF**  | 0.9962       | 0.9880                | 0.9880         | 0.9880       |
