# NLP Final Assignment
*As we use weka to implemente our application, there's actually no code but only configurations of classifiers and features. Besides, there are too many same configurations so we decide to only give the configuration by which the maximum score is achieved. Other configurations are only some feature and filter modifications based the given one.*
## Configuration
The best score is achieved by `Bigram + Word Embedding` with preprocessing and normalization as you can see in the report.
Its configuration is
```
weka.classifiers.meta.FilteredClassifier -F "weka.filters.MultiFilter -F \"weka.filters.unsupervised.attribute.TweetToEmbeddingsFeatureVector -S AVERAGE_ACTION -embeddingHandler \\\"affective.core.CSVEmbeddingHandler -K /Users/joy/wekafiles/packages/AffectiveTweets/resources/w2v.twitter.edinburgh.100d.csv.gz -sep TAB -I last\\\" -K 15 -red -stan -stemmer weka.core.stemmers.NullStemmer -stopwords-handler \\\"weka.core.stopwords.MultiStopwords \\\" -I 1 -U -tokenizer \\\"weka.core.tokenizers.TweetNLPTokenizer \\\"\" -F \"weka.filters.unsupervised.attribute.TweetToSparseFeatureVector -E 5 -D 3 -I 0 -F -M 0 -G 0 -taggerFile /Users/joy/wekafiles/packages/AffectiveTweets/resources/model.20120919 -wordClustFile /Users/joy/wekafiles/packages/AffectiveTweets/resources/50mpaths2.txt.gz -Q 2 -red -stan -stemmer weka.core.stemmers.NullStemmer -stopwords-handler \\\"weka.core.stopwords.MultiStopwords \\\" -I 1 -U -tokenizer \\\"weka.core.tokenizers.TweetNLPTokenizer \\\"\" -F \"weka.filters.unsupervised.attribute.Normalize -S 1.0 -T 0.0\" -F \"weka.filters.unsupervised.attribute.Reorder -R 4-last,3\"" -S 1 -W weka.classifiers.functions.LibLINEAR -- -S 1 -C 1.0 -E 0.001 -B 1.0 -L 0.1 -I 1000
```
which you can set in "Classify" -> “Classifier" -> double right click -> "Edit Configuration". Other configurations can be easily modified on the weka GUI according which features and classifier to use.
For balanced dataset we have configuration (adding a `SpreadSubsample` filter before any filter)
```
weka.classifiers.meta.FilteredClassifier -F "weka.filters.MultiFilter -F \"weka.filters.supervised.instance.SpreadSubsample -M 1.0 -X 0.0 -S 1\" -F \"weka.filters.unsupervised.attribute.TweetToEmbeddingsFeatureVector -S AVERAGE_ACTION -embeddingHandler \\\"affective.core.CSVEmbeddingHandler -K /Users/joy/wekafiles/packages/AffectiveTweets/resources/w2v.twitter.edinburgh.100d.csv.gz -sep TAB -I last\\\" -K 15 -red -stan -stemmer weka.core.stemmers.NullStemmer -stopwords-handler \\\"weka.core.stopwords.MultiStopwords \\\" -I 1 -U -tokenizer \\\"weka.core.tokenizers.TweetNLPTokenizer \\\"\" -F \"weka.filters.unsupervised.attribute.TweetToSparseFeatureVector -E 5 -D 3 -I 0 -F -M 0 -G 0 -taggerFile /Users/joy/wekafiles/packages/AffectiveTweets/resources/model.20120919 -wordClustFile /Users/joy/wekafiles/packages/AffectiveTweets/resources/50mpaths2.txt.gz -Q 2 -red -stan -stemmer weka.core.stemmers.NullStemmer -stopwords-handler \\\"weka.core.stopwords.MultiStopwords \\\" -I 1 -U -tokenizer \\\"weka.core.tokenizers.TweetNLPTokenizer \\\"\" -F \"weka.filters.unsupervised.attribute.Normalize -S 1.0 -T 0.0\" -F \"weka.filters.unsupervised.attribute.Reorder -R 4-last,3\"" -S 1 -W weka.classifiers.functions.LibLINEAR -- -S 1 -C 1.0 -E 0.001 -B 1.0 -L 0.1 -I 1000
```
## Dataset
We have one training dataset and one test set for final test. The dataset is already processed by Excel to meet the requirement of dataset for weka.
## Test Option
Please tick the "Supplied test set" option to choose the test for testing.
## Memory Usage
It's better to set the memory not too small in weka. 4GB works for us.
