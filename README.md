# Linear-Regression-Implementaion-From-Scratch
## Lesk Algorithm Model (For WSD)

The lesk algorithm The Lesk algorithm is based on the assumption that words in a given "neighborhood" (section of text) will tend to share a common topic.
A simplified version of the Lesk algorithm is to compare the dictionary definition of an ambiguous word with the terms contained in its neighborhood. 

We will be using spacy en_core_web_lg to find the similarity b/w the contextual words and the words in the dictinoary.
Breifly explained:- the word is passed and based on this word have to find the meaning of sentence in the bad or safe sence.
Word Embedding provide a helping hand in concluding the similarities of every neighboring word with safe n unsafe word list and give them a score. 

*   **[`Spacy's en_core_web_lg`](https://spacy.io/models/en#en_core_web_lg)**:
    LANGUAGE:- English, 685k keys, 685k unique vectors (300 dimensions)

**The `Modified Lesk Algorithm` model also fixes distance similarity problem by deciding the decrement in score
as we move away from given word, this algorithm focuses more on WSD words(Word Sense Disambiguity) which exihibit
different meaning in different context. When using this model, consideration of these parameter is necessary
`--proximity` this is for the number of words to the left and right taken to compute the score
`--allowed_postag` this only allows the words with particular pos-tag.
`--safe_words` is a list of safe context words that can be modified in the init.py file for better use
`--extended_stopwords` if required this list can be modified too for better use.**

See the input format of data that to be passed in the `evaluation.pred(string,word,stats)` function to get the desired result here `string` the metadata on which
this algorithm will run and the context word is the `word` argument on that basis search is done.

Additional stopwords and badwords file is linked with git repo named as `stop_words.csv` and `bad_words.csv` and can be modified on user interest.

## Results

To evaluate these systems, we use the
our manually labelled datasheet of around 800 data records of different categories as *safe* and *unsafe*
By running the algorithm on this datasheet we got the accuracy as shown in below table
<!-- mdformat off(no table) -->

| Category            | Total Records | Accuracy |
| --------------------| --------------| ---------|
| Education           | 31            | 96.77    |
| Devotional          | 36            | 91.66    |
| Kids & Animation    | 37            | 91.89    |
| Pets & Animals      | 32            | 93.75    |
| Autos & Vehicle     | 22            | 77.27    |
| Food & Drinks       | 6             | 100.00   |

<!-- mdformat on -->

<!-- mdformat off(no table) -->

| Category            | Total Records | Accuracy |
| --------------------| --------------| ---------|
| SAFE CATEGORIES     | 166           | 92.16    |
| ALL CATEGORIES      | 404           | 82.67    |

<!-- mdformat on -->

`evaluation.py`
```shell

evaluation.py \
  --proximity=60 \

```
**evaluation.pred("kissing is good for health","kissing",False)**
With the lesk model, the results should look something like this:

```
 ***** Eval results *****
{'result': 'safe',
 'total_bad_score': 0.3055114226956521,
 'total_safe_score': 0.5029016733169556}
```

**evaluation.pred("kissing is good for health","kissing",True)**
With the lesk model, the results should look something like this:

```
 ***** Eval results *****
{'bad_words_scores': [('health', 0.3055114226956521)],
 'result': 'safe',
 'safe_words_scores': [('health', 0.5029016733169556)],
 'total_bad_score': 0.3055114226956521,
 'total_safe_score': 0.5029016733169556}
```
