# NLP-Based-Semantic-Analysis-on-Youtube-Comments-Dataset

## Introduction
In this notebook, I have a dataset of user comments for youtube videos related to animals or pets. I will attempt to identify cat or dog owners based on these comments, find out the topics important to them, and then identify video creators with the most viewers that are cat or dog owners.

## Data and Code
The dataset is too hugh to upload to the repo. You can download [here](https://drive.google.com/file/d/1o3DsS3jN_t2Mw3TsV0i7ySRmh9kyYi1a/view). The code is from [here](https://databricks-prod-cloudfront.cloud.databricks.com/public/4027ec902e239c93eaaa8714f173bcfc/1772353219017266/3842882422099798/105392983207357/latest.html).

## Some notes
- The embedding matrix/weight matrix for the embedding layer is truly what we want because it gives us embedding representation for each vocabulary, no matter what the output is(it gives context information, that's all).

## Summary
- Used a dataset of user comment for youtube videos related to pets (data size around 6M+) to parse out and analyzed text via Spark.
- Bulit a machine learning pipeline, labeled each comments after data cleaning by extracting key tokens (containing regex-Tokenizer module and key words setting) and imported Word2Vec module to word embeddings.
- Trained classifier models for the cat and dog owners with the best model (AUC score = 0.94).
- Extracted important topics (topic modeling) among cat and dog owners based on word frequency and identified creators with cat and dog owners in the audience for potential recommendation.
