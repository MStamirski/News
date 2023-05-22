# News
Natural Language Processing

The goal of this project was to build a model predicting whether a piece of news is fake or real. Data come from 3 sources:

https://www.kaggle.com/datasets/saurabhshahane/fake-news-classification

https://www.kaggle.com/datasets/clmentbisaillon/fake-and-real-news-dataset

https://www.kaggle.com/datasets/algord/fake-news

The project consists of 4 notebooks.

### DataPrep

Titles of news in four datasets were analysed, unnecessary columns were removed, as well as rows with nulls in title or label. Common label 'real' means that news are not fake. Titles were transformed by deletion of punctuation (extended for this project on the basis of data analysis), using lowercase, tokenization, deletion of stopwords (also extended) and lemmatization. Transformed titles were saved in new column 'news'. Then datasets were concatenated. It turned out that there were several empty news after transformation, so these rows were removed. Final dataset contained 139.662 news, 64.264 of which were fake and 75.398 were real. It was saved to csv file.

### BagOfWords

Two method of vectorization were used: CountVectorizer (which returns vectors with integer values meaning number of given word appearance in text) and TfIdf (wchich returns float values based also on word appearance in whole dataset). For separated real and fake news the most important words were counted and presented in two word clouds. Then prediction was conducted, using LGBMClassifier. F1 score was equal 0.70. A similiar prediction was performed for news vectorized by TfIdf. It turned out, that the result was identical.

### Embedding

Number of features resulted from unified length of sentences (25 words). Value of each feature was an index in vocabulary of word in sentence. Vocabulary size was limited to 10.000 of words, out of total almost 40.000. Used embedding model transformed each sentence to vector of 20 numbers. Then three neural network models were tested. Unfortunatelly, as learning curves show, number of features turned out to be unsufficient. The best model, with 3 dense layers and without RNN and Dropout layers, gave F1 score of only 0.64.

### SentenceTransform

News were transformed using SentenceTransformer model. Obtained vectors were features for training classification model based on Logistic Regression, which hiperparameter was tuned using Optuna. The F1 score achieved 0.72, which was the best result among other trials in this project. Then, based on predicted probabilities, the best threshold separating label 0 and 1 was found. It turned out to be 0.5, so this attempt didn't improve the result. At the end, using cosine distance in vector space, news similiar to several randomly selected ones were found.

### Words in fake news

### Words in real news
