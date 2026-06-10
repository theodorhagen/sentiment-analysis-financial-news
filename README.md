# Report

## Task 1: Exploratory Data Analysis

To explore the data we first looked at the distribution of the sentiment classes. From that we could see that most of the sentences were labelled neutral (about 60%), positive datapoints came in second (with 28%), while negative sentences were the fewest (about 12%). Since this is a highly imbalanced dataset, a classifier trained on it, may favor labelling more sentences neutral to keep a high accuracy. Furter on we decided that the overall accuracy metric may not be that meaningful, and that we should instead look at confusion matrices aswell as calculating an F1-Score.  
We then plotted the length of the sentences in words or rather tokens aquired from the ntlk tokenizer in a distribution plot. The distribution shows that a typical sentence in this dataset ranges between 12 and 30 words. The peak of the histogram (the mode) sits right around 18 to 22 words per sentence. The graph exhibits a distinct right-skewed distribution. While very few sentences contain fewer than 5 words, there is a long trailing tail extending past 50 words, with a maximum length stretching all the way to over 80 words. Because the sentence lengths are consistently constrained (mostly under 50 words), a Bag-of-Words or TF-IDF vectorizer will not suffer from severe document-length scaling issues. The text is uniformly dense with sentiment signals.  
We then computed the bigrams of every class individually. An initial analysis reveals a massive overlap in top bigrams across all three sentiments. Combinations relating to reporting currencies, figures, and standard financial terms (e.g., "eur num", "num mn", "net sale") dominate the frequencies everywhere. This indicates that general financial vocabulary alone is sentiment-neutral; a classifier cannot rely on terms like "operating profit" or "net sale" by themselves to make a prediction, as they appear consistently regardless of sentiment.  
In the negative class, distinct directional and risk-associated anchors begin to surface. The appearance of the bigram "down from" provides a strong, explicit linguistic cue of decline. Furthermore, "compared to" and "corresponding period" rank highly here, suggesting that negative sentiment in corporate reporting is frequently framed through historical comparisons.  
The positive sentences contain a highly predictive, unambiguous directional bigram: "rose to". This action-oriented verb phrase acts as a primary feature for sentiment classification. Additionally, the baseline term "operating profit" ranks noticeably higher in the positive class (Rank 7) compared to the neutral class (Rank 16), indicating that the sheer mention of operating profits is more heavily skewed toward positive corporate growth announcements.  
The neutral class is uniquely characterized by objective, passive, and forward-looking journalistic language. Bigrams like 'according to' and 'company said' point directly to purely informative or factual press reporting.  
In conclusion, because the unique sentiment carriers (like "rose to" or "down from") are much less frequent than the massive baseline financial noise (like "eur num"), a TF-IDF classifier will need to heavily penalize the shared financial jargon using document frequency filters, allowing the model to focus on the highly specific directional verbs that actually dictate the sentiment.

## Task 2: Text Preprocessing

For the text proprecossing, we adopted a pipeline consisting of multiple steps, namely:

- Lowercasing
- Denoising
- Stop Word Removal
- Lemmatization
- Only ASCII
- Number Removal

The Lowercasing is done with a simple python for loop, and it is supposed to make the texts more comparable.  
The Denoising step required a deeper look into the dataset, to see what kind of characters the sentences contain aswell as looking at certain word contractions. Some examples for characters that got removed are brackets, commas, currency symbols, and percent symbols. We also cleaned up the word contractions such as "haven"t" and changed them to "have not".  
For the Stop Word Removal we used the inbuilt stop word list of nltk, although we removed and added some word to the final stop word list we employed. Words that were in the original nltk list, but we did not want in our stop word list were words such as "above", "up", "over", "below", "down", "under", "no", "not", and "nor" since these may be very relevant in the upcoming sentiment classification tasks. Some stop words were added by hand, since we did not find them to be useful for the classification, namely "bln", "mln", "pct", and "percent".  
For the Lemmatization we used the ntlk WordNetLemmatizer, and just lemmatized every word (after tokenizing the sentences into words).
Since there were some non ASCII characters, such as letters which are not in the standard english alphabet, we thought it was a good idea to remove them, in the case that they could cause problems later in the line. These were only found in names of places, companies, and brands, which is why the actual names of these aren"t important.  
While the final step, Number Removal, may seem counterintuitive for a sentiment classification task, at least for feature engineering methods such as Bag of Word or TF-IDF which can handle numbers better if they are just all replaced with "\<NUM>", it is useful. For Task 5, when we trained our classifier using pre-trained language models, this final step of the preprocessing pipeline may be omitted.

## Task 3: Sentiment Classification

## Task 4: Textual similarity

## Task 5: Pre-trained Language Models
