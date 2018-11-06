# ShortText-Fasttext

ShortText classification is an intractability problem in Machine Learning. Based on Facebook's Fasttext, this project optimizes its performance in ShortText and introduces a mechanism named category dropout. This mechanism works very well in Weibo's ads classification. Details about category dropout can read [Blog](https://blog.csdn.net/AckClinkz/article/details/81907903)。

# Building

```shell
git clone https://github.com/AckClinkz/ShortText-Fasttext
cd ShortText-Fasttext
make
```
# Use

This section assumes that you are somewhat familiar with Fasttext. You can try to learn the basics of Fasttext from [officical website](https://github.com/facebookresearch/fastText).

Category Dropout only supports mode of `supervised`. Train model with category dropout, just set `-cate_dropout`.

In pratice, setting minCount can improve model performance. But it will lost infomation in low-frequency word. Settting vocabulary is an efficient method to balance them. If word in vocabulary, don't consider minCount.

Summarize the above points ShortText-Fasttext's usage as follows:

```
fasttext supervised \
  -input your_input.txt \
  -output your_model \
  -dim 120 \
  -lr 0.3 \
  -wordNgrams 3 \
  -minCount 30 \
  -bucket 10000000 \
  -epoch 100 \
  -thread 4 \
  -cate_dropout \
  -vocab ./your_vocabulary.txt
```

# Update 2018.11.6

According to [《Item2Vec: Neural Item Embedding for Collaborative Filtering 》](https://arxiv.org/vc/arxiv/papers/1603/1603.04259v2.pdf), realize `item2vec`, usage as follow:

```
fasttext skipgram_item2vec \
  -input ./your_input.txt \
  -output "./your_model" \
  -ws 5 \
  -dim 120 \
  -lr 0.01 \
  -wordNgrams 1 \
  -minCount 2 \
  -bucket 1000000 \
  -epoch 5 \
  -thread 8
```
