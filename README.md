# NLP-Based-Semantic-Analysis-on-Youtube-Comments-Dataset

## Introduction
In this notebook, I have a dataset of user comments for youtube videos related to animals or pets. I will attempt to identify cat or dog owners based on these comments, find out the topics important to them, and then identify video creators with the most viewers that are cat or dog owners.

## Data and Code
The dataset is too hugh to upload to the repo. You can download [here](https://drive.google.com/file/d/1o3DsS3jN_t2Mw3TsV0i7ySRmh9kyYi1a/view). The spark code is from [here](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/1772353219017266/3842882422099798/105392983207357/latest.html). The skip-gram jupyter notebook on my test data has been uploaded to the folder.

## Notes
- The embedding matrix/weight matrix for the embedding layer is truly what we want because it gives us embedding representation for each vocabulary (on each row), no matter what the output is (it just gives predicted output, that's all).
- Be aware how to define an embedding for a given review (just a little more upon word embedding). Here token are just each word. What Word2Vec does is to map each word to a unique fixed-size vector and then transform each document into a vector using the average of all words in the document.
- About skip-gram, we pass in a word and try to predict the words surrounding it in the text.
- In skip-gram, I create two dictionaries to convert words to integers and back again (integers to words). This is a little bit similar to baby-gpt project.
- Subsampling in skip-gram is for removing some of the noise. The higher a word may appear, the higher it will be removed.
- Batches and window: example

```
Say, we have an input and we're interested in the idx=2 token, 741:
[5233, 58, 741, 10571, 27349, 0, 15067, 58112, 3580, 58, 10712]
For R=2, get_target should return a list of four values:
[5233, 58, 10571, 27349]
```
When generating batch, the idea is that it grabs batch_size words from a words list. Then for each of those batches, it gets the target words in a window. Inputs are like [0, 0, 0, 1, 1, 1, 2, 2, 2, 3, 3, 3] if batch_size = 4 and targets are like [1, 2, 3, 0, 2, 3, 0, 1, 3, 0, 1, 2].

- I use T-SNE to visualize word vectors.
- In the prediction part, I want to know if a model can tell whether a people is cat or dog owner. Before that, I manually label the data with keywords matching technique. And the input to the machine learning model is just the document embedding.
- For topic modeling, I extract the five most related topic that an owner might be interested in. For video creator recommendation, I pick the 3 videos (with authors) with the most reviews.
- For LDA, basically, each document is made up of various words, and each topic also has various words belonging to it. Sort the words with respect to their weight score, the top x words are chosen from each topic to represent the topic.
  
## Summary
- Used a dataset of user comment for youtube videos related to pets (data size around 6M+) to parse out and analyzed text via Spark.
- Bulit a machine learning pipeline, labeled each comments after data cleaning by extracting key tokens (containing regex-Tokenizer module and key words setting) and imported Word2Vec module to word embeddings.
- Trained classifier models for the cat and dog owners with the best model (AUC score = 0.94).
- Extracted important topics (topic modeling) among cat and dog owners based on word frequency and identified creators with cat and dog owners in the audience for potential recommendation.
