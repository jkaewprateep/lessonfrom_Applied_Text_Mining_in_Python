# University of Michigan - Applied Text Mining in Python - notes
University of Michigan - Applied Text Mining in Python

## This note we aim to study text mining and I found interesting of text mining applications from the course examples including medical records and social media as sources.

### 🧸💬 Sample of input data
💃( 👩‍🏫 )💬 For text mining solution the problem is there are many text string formats for the scopes since the translation is a step of understanding. </br>
🦤💬 Since the handwriting problem text mining was introduced by NTLK for pattern learning as a token and normalizer. It can use to find most frequently used word and similarity after we had clean up of the input data to find the meaning and data pattern  </br>
🧸💬 Sample data from hospital for migration of text inputs database records in wide formats into database-capable fields. </br>
🐐💬 There are many datetime data input patterns we need to consider from the examples, ```dd/mm/yyyy```, ```d/m/yyyy```, ```mm/dd/yyyy```, ```m/d/yyyy```, ```mm/dd/yy```, ```m, yyyy```, ```yyyy``` and etc. </br>

#### Expression condition (1)
🐑💬 ➰ The datetime filed must contained in the same word ```( ... )``` and they can be start of the word in the sentence or not ```(?:...)``` and they are contained of the patterns inside ```( ... | ... | ... )```  </br>
🦭💬 The field may contain of digits from one to two characters, ```\d{1,2}```, and the separator may contain these characteristics ```\/|-``` or not. </br>
🦭💬 The tab fields next to the oscillatory field contain of digits from one to two and next in two to four digits characters.  </br> ```\d{1,2}```, ```\d{2,4}``` </br>


```
0         03/25/93 Total time of visit (in minutes):\n
1                       6/18/85 Primary Care Doctor:\n
2    sshe plans to move as of 7/8/71 In-Home Servic...
3                7 on 9/27/75 Audit C Score Current:\n
4    2/6/96 sleep studyPain Treatment Pain Level (N...
5                    .Per 7/06/79 Movement D/O note:\n
6    4, 5/18/78 Patient's thoughts about current su...
7    10/24/89 CPT Code: 90801 - Psychiatric Diagnos...
8                         3/7/86 SOS-10 Total Score:\n
9             (4/10/71)Score-1Audit C Score Current:\n
dtype: object
```


###  🧸💬 String matching method
👧💬 🎈 Iterations of input as a sequence of words from input source as text. </br>
🦤💬 There are some problems found by ```str.equal``` or white space problems by verifying that the expression string is easy and transferable. </br>
👧💬 🎈 There is well-known news about object string return verification by the summary method that many programmers are using to verify the outputs from accounting applications and authentication they have found that it is faster but it will not correct in some cases, not because of change of the characters and haze summing number verification but the correct result set may not be equal for multiple times trials. </br>
👨🏻‍🏫💬 Summarized is one input for the verification method ...  </br>

```
for idx, item in enumerate(doc) :
    item = item.strip();
    match_string_one = r"((?:\d{1,2})(?:(?:\/|-)\d{1,2})(?:(?:\/|-)\d{2,4}))";
    answer_one = re.search(match_string_one, item);
```


#### Expression condition (2)
🐨🎁🎵🎶 Maximum of two characters digit contained or name of one of these month field word container ```Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec``` with one or multiple of a small capital letter. Possible repeating of these separators ```- or . or \ or , ```. They may contain two to four character digits. </br>

```
match_string_two = r"((?:\d{,2}\s)?(?:Jan|Feb|Mar|Apr|May|Jun|Jul|Aug|Sep|Oct|Nov|Dec)[a-z]*(?:-|\.|\s|,)\s?\d{,2}[a-z]*(?:-|,|\s)?\s?\d{2,4})";
```

#### Expression condition (3)
🐯💬 The datatime field may start with digit characters from one to two attached with the phaser contaned ```- or /``` or ```4 digits``` </br>

```
match_string_the = r"((?:\d{1,2}(?:-|\/))?\d{4})";
```

### 🧸💬 String matching results - transform of a datetime data fields for a filter.
```
0        9
1       84
2        2
3       53
4       28
      ... 
495    231
496    141
497    186
498    161
499    413
Name: original row number, Length: 500, dtype: int64
```

## 🦤💬 Lexical diversity - evaluate the richness of word resources input diversity, well-organized dialogues had their patterns and number of frequent words used can determine the dialogue characteristics.

```
import nltk

nltk.data.path.append("assets/")   # 🧸💬 Working directory to find resources if there are any.

# 🧸💬 Reading file and stored into a local variable.
with open('assets/document.txt', 'rt', encoding="utf8") as file: 
    _document = file.read()

# 🧸💬 Breaks input document into sentences, words and phases.
tokensfrom_document = nltk.word_tokenize(_document);

# 🧸💬 Create text object document for reference.
text1 = nltk.Text(tokensfrom_document);

# 🧸💬 Couting and identifying words used frequently.
fdist = nltk.FreqDist(text1); 

# 🧸💬 Display top 20 from word appearances.    
fdist.most_common(20);
```

### 🧸💬 Example of the words used frequent output
```
[(',', 19420),
 ('the', 18698),
 ('.', 16624),
 ('to', 12149),
 ('and', 11400),
 ('a', 8979),
 ('of', 6510),
 ('is', 5699),
 ('in', 5109),
 ('his', 4693),
 ("'s", 3682),
 ('her', 3674),
 ('he', 3556),
 ('that', 3517),
 ('with', 3293),
 ('him', 2570),
 ('for', 2433),
 ('by', 2321),
 ('The', 2234),
 ('on', 1925)]
```

## 🦤💬 Whitespaces per sentence of the dialogue document is one of the characteristics indicated of languages, commonly used of word organize applications, document types, age and proficiency, and sometimes including para-phases detection paragraph.
👧💬 🎈 Application on para-phrase, word vectors, vectors categorized and plotting of word vector dimension can help about find sources or identify products of the generators. </br>
🐐💬 There is a shuffling method to control of both working team, product, process, and identify identification but the application is typical because of culture and traditional or organization and individual </br>

```
text1_reconstituted = ' '.join(list(text1))

tk = WhitespaceTokenizer();                        # 🧸💬 For creating word token (separator characteristic ) from whitespaces string formats.
_temp = tk.tokenize(text1_reconstituted);          # 🧸💬 Apply token on the text string object. 

numberof_whitespaces = len(_temp);                 # 🧸💬 Find number of words by whitespace.

#################################################################
_temp = nltk.sent_tokenize(text1_reconstituted)    # 🧸💬 For creating stntence token.
numberof_sentences = len(_temp);                   # 🧸💬 Find number of sentences from the text object.
```

## 🦤💬 Phases of the sentence or representing is one identification not only the identify of similar or repeating words but source identification or significant process identifications.
🦤💬 Lambda function benefits for multiple steps to a solution with the method applicable.  </br>
👨🏻‍🏫💬 There are many public speakers who repeat about removed category person by using the function, this function is work capable of compiler the same and is applicable in a wide ranges of programming syntax support and readable command syntax for programming learners.  </br>
🐑💬 ➰ How do we build a summarize function in a paragraph without alpha ⁉️  </br>
🐐💬 The meaning of alpha, beta, and gamma for programming versions is not only majority number but approximately method. The approximate method is not an approximate value but it works with the primary function for absolute results. </br>
👧💬 🎈 This is alpha in software development, working with the primary function. How is the alpha in real life ⁉️  </br>

```
from nltk.tag import pos_tag;
import collections;

part_ofspeech = pos_tag(text1);                                                     # 🧸💬 Identify phases from sentences by frequently used or attached influences.
count_partofs = collections.Counter( (speech[1] for speech in part_ofspeech) );     # 🧸💬 Identify a number of the part of speech found from the previous line.

sorted(count_partofs.most_common(5), key=lambda x: x[1], reverse=True);             # 🧸💬 Display top 5 frequent used part of speech found in the sentences from the document example.
```

## 🦤💬 NLTK n-grams, unigrams, bigrams, Jaccard distance, and explain of how you find the most matching word or next phase character for sentence and word approximation.
🧸💬 Does someone try to use neuron network's Dense layer to quickly learning of word simialrity⁉️  </br>
🧸💬 All are prediction values and we do not need to compare a different set of inputs for the current velocity, how is the faster way to have an evaluation from this approach ⁉️  </br>
🐑💬 ➰ N-grams as in ChatGPT⁉️ 🧸💬 No N-grams is not word similarity predictions or word phase predictions but it is tokens words from input words or sentence it require some method input to make predictions result  </br>

```
🏁 🐑💬 ➰ Unigram 👁️‍🗨️🐣💬 Bigram
nltk.ngrams(entry, n=3)       # 🧸💬 Example of phase entry into 3 phases if possible.
nltk.ngrams(entry, n=4)       # 🧸💬 Example of phase entry into 4 phases if possible.
nltk.ngrams(entry, n=5)       # 🧸💬 Example of phase entry into 5 phases if possible.
```

## 🦤💬 Attention networks we can use to find attenuation of words near the similarity.
🐑💬 ⁉️ It had the reflection side ⁉️ 🦤💬 Yes that is because we can use both reversed and uniword.  </br>
🐯💬 IF one word you can phase. </br>

<p align="center" width="100%">
    <img width="50%" src="https://github.com/jkaewprateep/lessonfrom_Applied_Text_Mining_in_Python/blob/main/06.png">
</p>

```
from nltk import jaccard_distance;

# 🧸💬❤️ Calculation of distance of edit to companions the similarity.
jaccard_distance( set(nltk.ngrams(entry, n=3)), set(nltk.ngrams(item, n=3))

from nltk import edit_distance;

# 🧸💬❤️ Calculation of distance of edit to fullfilled the similarity.
edit_distance( entry, item, transpositions=True ), item )
```

<p align="center" width="100%">
    <img width="100%" src="https://github.com/jkaewprateep/lessonfrom_Applied_Text_Mining_in_Python/blob/main/07.png">
</p>

## 👨🏻‍🏫💬 Linear regressions for text sequence data and linear model learning from text vectorize optimizer.

```
from sklearn.naive_bayes import MultinomialNB
scaler = CountVectorizer().fit(X_train);                         # 🧸💬 Define the linear model you need to perform a function,
                                                                 # there are interesting and famous for the flower clan 🥀📻
                                                                 # is power scales because all are the power for them.
scaler_xtrain = scaler.fit_transform(X_train);                   # 🧸💬 Training for weight momentum can be used for prediction.
scaler_xtest = scaler.transform(X_test);                         # 🧸💬 Equivalent to np.reshape() or tf.reshape() specific cond
                                                                 # for use as input prediction function.

scaler_NB = MultinomialNB(alpha=0.1);                            # 🧸💬 Another function model, normalize with alpha = 0.1.
                                                                 # 🦭💬 Similar to learning rates think about a goat jumps
                                                                 # across a river of mountains 🐑💬 ➰ Baaaeeeeeee !~
scaler_NB = scaler_NB.fit(scaler_xtrain, y_train);               # 🧸💬 Traning for weight momentum.

predictions = scaler_NB.predict_proba(scaler_xtest)[:, 1];       # 🧸💬 Prediction and the result, ( label, "array as result" )
```

## 👨🏻‍🏫💬 TfidfVectorizer for updating document with words appearance company with learning document.

```
from sklearn.feature_extraction.text import TfidfVectorizer

tfidf = TfidfVectorizer().fit(X_train);                          # 🧸💬 Create object for word-in out documents companions.
feature_names = np.array(tfidf.get_feature_names());             # 🧸💬 Create an array of features name.

scale_tfidf = tfidf.transform( X_train );                        # 🧸💬 Transfrom of the input shape as array property.
max_tfidf = scale_tfidf.max(0).toarray()[0];                     # 🧸💬 Find maximim number of axis to array.
sorted_tfidx = max_tfidf.argsort();                              # 🧸💬 Sort by argruments, for substitution in next.
sorted_tfidf = max_tfidf[sorted_tfidx]                           # 🧸💬 Dataset selection from sorted arguments.

smallest_tfidf = pd.Series( sorted_tfidf[:20], index=feature_names[sorted_tfidx[:20]]); # 🧸💬 Smallest.
largest_tfidf = pd.Series( sorted_tfidf[-20:][::-1], index=feature_names[sorted_tfidx[-20:][::-1]]); # 🧸💬 Largest.
```

## 👨🏻‍🏫💬 Integration area from word similarity, how do we optimize speech engines from learning input approximation?
🦤💬 The steady area indicates learning and processing, errors, and commons in real-time for optimization and development. </br>

```
from sklearn.metrics import auc;

tfidf = TfidfVectorizer(min_df=3);                               # 🧸💬 Create TFid object with minimum 3 words appearnce.
vectorNB = MultinomialNB(alpha=0.1);                             # 🧸💬 Create Multinomial model with alpha = 0.1
                                                                 # 🧸💬 Polynomail with multi-coefficients.
vectorNB.fit(tfidf_X_train, y_train);                            # 🧸💬 Traning for weights momentum.

tfidf_X_train = tfidf.fit_transform(X_train);                    # 🧸💬 Array shape property reshape for prediction and train.
tfidf_X_test = tfidf.transform(X_test);                          # 🧸💬 Array shape property reshape for prediction.
predictions = vectorNB.predict_proba(tfidf_X_test)[:, 1];        # 🧸💬 Prediction from transformed, (label, "array values")

roc_auc_score(y_test, predictions);                              # 🧸💬 Integration curve and area under curve, Proxima value.
```

## 👨🏻‍🏫💬 Sometimes to start implementation a simple one-hot implement method can applied with embedded value in the system.
👧💬 🎈 Expectations scales selection, the good indicator is divided by half when it starts.  </br>

```
document_spam = spam_data[spam_data["target"] == 1];             # 🧸💬 Pandas selection for spam target email.
document_nonspam = spam_data[spam_data["target"] != 1];          # 🧸💬 Pandas selection for non-spam target email.

document_spam["lenght"] = document_spam["text"].apply( lambda x: len(x) );  # 🧸💬 Create array of lenght from its input.
avg_length_document_spam = document_spam["lenght"].mean();                  # 🧸💬 Aveage value of the array create previolusly.

document_nonspam["lenght"] = document_nonspam["text"].apply( lambda x: len(x) ); # 🧸💬 Create array of lenght from its input.
avg_length_nondocument_spam = document_nonspam["lenght"].mean();                 # 🧸💬 Aveage value of the array create previolusly.
```

## 🦤💬 There is a problem when we need to add some property after a trained model or program has been created, this method can add of new feature and transfer it as a sparse value ( discrete ) for calculation. 
👧💬 🎈 This is remarks since sparse, logistic, categorized, and logit shapes are sensitive inputs for learning model and matrix operations.  

```
def add_feature(X, feature_to_add):
    """
    Returns sparse feature matrix with added feature.            # 🧸💬 Create float number networks input from features.
    feature_to_add can also be a list of features.
    """
    from scipy.sparse import csr_matrix, hstack
    return hstack([X, csr_matrix(feature_to_add).T], 'csr')      # 🧸💬 Horizontal stack of compressed sparse matrix input.
```

👧💬 🎈 Add the length of the input, and the length of digits in the input as features. The digits input threshold is a magic number called the golden number used for simulation but not as an indicator. </br>
🐐💬 Precision number and round number are not similar meaning working with information needs to work with estimate scope and the objective of the message for information extraction. </br>
🐑💬 ➰ Summation and polynomial coefficients are simple methods for verifying decrypt reading messages after a few steps of verification a tablet ruler table can work on a logarithms scale that is because of defussion is added into a summary. It is signatures. </br>

```
# 🧸💬 Applying feature add function for creating new input sparse result from the current.
X_traintfidf_length = add_feature(X_traintfidf, [ X_train.str.len(), X_train.apply( lambda x : len( [digit for digit in x if digit.isdigit() ]) ) ]);
```

👧💬 🎈 The nonword character count indicates attention or significance of the communication message sometimes is hour, minute, and precision word. </br>
🦭💬 They are sending medical prescripts in communications for test of the communication because they contain precision values and summarize fast categories for known communicators. </br>
🐨🎁🎵🎶 Shall us send more medical prescripts ⁉️  🦁💬 They will be a good sleeping pills for communicators. </br>

```
# 🧸💬 Create new sparse input by add new feature, a none-word count feature.
scaler_X_train_length = add_feature(scaler_X_Train, [ X_train_limited.str.len(), 
                                                      X_train_limited.apply( lambda x : len( [digit for digit in x if digit.isdigit() ]) ), 
                                                      X_train_limited.str.findall(r'(\W)').str.len() ]);
```

## 🦤💬 Documents para-phrase, document similarity and journeys paradigms 
👧💬 🎈 Word and Wordnet lexical dictionary using ```nltk``` and ```nltk.corpus``` for word corpus dictionary applies for document similarity or word para-phase scores evaluation. </br>

```
def document_path_similarity(doc1, doc2):
    """Finds the symmetrical similarity between doc1 and doc2"""

    synsets1 = doc_to_synsets(doc1)
    synsets2 = doc_to_synsets(doc2)

    return (similarity_score(synsets1, synsets2) + similarity_score(synsets2, synsets1)) / 2
```
