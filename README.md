## Spam or Ham Text Classification
<p align="center"> 
   <img width="1000" height="400" alt="Ekran Resmi 2021-06-28 01 15 28" src="https://user-images.githubusercontent.com/87663976/149565085-ee51ff21-b0be-4e74-a00d-4d2595247349.png">
</p>

This is a text classification project.The tsv format dataset we have  the SMS Spam Collection is a set of SMS tagged messages that have been collected for SMS Spam research. It contains one set of SMS messages in English of 5,574 messages, tagged according being ham (legitimate) or spam.

In this project, I cover some basics of natural language processing like reading in and creating structure in messy text data, and then cleaning and tokenizing that data. Then the project will cover some of the topics like lemmatizing, stemming, and vectorizing the data. In other words, converting it from text into a numeric matrix.


# Data Preprocessing

First I created a data frame from unstructured text data with label and body text columns. After that, I applied a function to my text column to remove punctuation. The reason that we care about punctuations is they look like just another character to Python. But realistically, they don’t help pull the meaning out of a sentence. When I'm done with removing functions I got into tokenization and I use the \W+ regex that will split wherever it sees one or more non-word characters to create a list of tokens.

I had one more important thing to deal with which is stopwords. Stopwords are like punctuations too. They are commonly used words (like the, but, if) but they don’t contribute much to the meaning of a sentence. So it's better to remove them, to limit the number of tokens Python has to look at when building our model.



# Stemming and Lemmatizing

I applied both stemmer and lemmatizer methods to my text data to see the difference between them. They are both very important when dealing with text data but we can say lemmatizing the text is more efficient in most situation. But it's safe to note it is slower than stemming because it is more complex.

# Vectorizing

The process that we use to convert text to a form that Python and a machine learning model can understand is called vectorizing. This is defined as the process of encoding text as integers to create feature vectors. In this part, I applied three different vectorizing methods to my data (Count vectorization, N-gram vectorizing, and TF-IDF). The photo below shows TF-IDF vectorizing:

<p align="center"> 
   <img alt="Ekran Resmi 2021-06-28 01 15 28" src="https://user-images.githubusercontent.com/87663976/149574490-0a292b84-53f1-4092-99d6-f926abd2eb5a.png">
</p>

## Feature Engineering
Feature engineering is the process of creating new features and/or transforming existing features to get the most out of your data. What else could O extract from that text that would be helpful for the model to decide spam from ham? For instance, I thought to include the length of the text field. Maybe spam tends to be a little bit longer than real text messages. And then I included what percent of the characters in the text message is punctuation. I added these new features to the data and to see if they were relevant for our upcoming machine learning model I used some visualizations.The first photo shown above is for the newly created text length feature for the distribution of spam/ham messages and the second photo is for the percentage of punctuations:

<p align="center"> 
   <img src="https://user-images.githubusercontent.com/87663976/149577938-bed6228d-9f2e-4274-8eac-0ea89baaa7e6.png">
</p>


<p align="center"> 
   <img src="https://user-images.githubusercontent.com/87663976/149577981-89afbc97-1c4d-434a-9247-525dd4bb2ab4.png">
</p>

I chose the text length feature as my new feature and left the punctuation percentage behind after a few observations.

# Cross-validation and Evaluation Metrics

Clean up the data based on previous chapters and this time we use TF-IDF to vectorize the data, then split data into actual features and labels. First I observed cross-validation scores with k-fold (k=5). K-fold facilitate the splitting of our full data set into the 5 subsets and then this cross_val_score got me actual scores.

# Random Forest Model on Holdout Test Set

After I got the results of cross-validation I trained my random forest model Random Forest with Holdout Test Set and checked for the most important features. The body_legth feature I created and added to the dataset turned out to be the most important feature. Then I got the scores for my random forest model.
   |     Precision        | Recall       |      F-Score |
   | :------------------: | :----------: | :-----------:|
   |  1.0                 | 0.5797       | 0.7339       |
  
Then I checked the best parameters combinations for my random forest model with grid-search.

 

