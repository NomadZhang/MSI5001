# Dataset Description
This dataset is about twitter posts of airline passengers regarding the service of 6 different US airlines they have travelled with. Each tweet contains the original post, the sentiment of the post and confidence score of that assigned sentiment label.

# Clustering Task:
- Suppose, the "airline_sentiment" column is not given; you simply know that there are supposed to be three types of tweets
- If you now perform clustering on the text samples, ideally each cluster should represent one of the three classes
    - Ideally, each of your cluster should contain samples from one class only
    - But you may get some samples from other classes as well; are they low confidence samples? Most likely. Will be interesting to check this out

# Expected Task Description
- You can only use the sample labels ("airline_sentiment" column) for verifying your clustering output
- You should perform cleaning of the textst
- Since you need to cluster text samples, you need to transform each text sample into a feature vector:
    - can explore text representation techniques
    - can explore text summary feature extraction traditional techniques
    - can explore language models
- You should explore different clustering techniques and dimension reduction techniques