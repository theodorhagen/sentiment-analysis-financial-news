# Report

## Task 1: Exploratory Data Analysis

## Task 2: Text Preprocessing

For the text proprecossing, we adopted a pipeline consisting of multiple steps, namely:

- Lowercasing
- Denoising
- Stop Word Removal
- Lemmatization
- Only ASCII
- Number Removal

The Lowercasing is done with a simple python for loop, and it is supposed to make the texts more comparable.  
The Denoising step required a deeper look into the dataset, to see what kind of characters the sentences contain aswell as looking at certain word contractions. Some examples for characters that got removed are brackets, commas, currency symbols, and percent symbols. We also cleaned up the word contractions such as "haven't" and changed them to "have not".  
For the Stop Word Removal we used the inbuilt stop word list of nltk, although we removed and added some word to the final stop word list we employed. Words that were in the original nltk list, but we did not want in our stop word list were words such as "above", "up", "over", "below", "down", "under", "no", "not", and "nor" since these may be very relevant in the upcoming sentiment classification tasks. Some stop words were added by hand, since we did not find them to be useful for the classification, namely "bln", "mln", "pct", and "percent".  
For the Lemmatization we used the ntlk WordNetLemmatizer, and just lemmatized every word (after tokenizing the sentences into words).
Since there were some non ASCII characters, such as letters which are not in the standard english alphabet, we thought it was a good idea to remove them, in the case that they could cause problems later in the line. These were only found in names of places, companies, and brands, which is why the actual names of these aren't important.  
While the final step, Number Removal, may seem counterintuitive for a sentiment classification task, at least for feature engineering methods such as Bag of Word or TF-IDF which can handle numbers better if they are just all replaced with "\<NUM>", it is useful. For Task 5, when we trained our classifier using pre-trained language models, this final step of the preprocessing pipeline may be omitted.

## Task 3: Sentiment Classification

## Task 4: Textual similarity

## Task 5: Pre-trained Language Models
