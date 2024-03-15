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

## 🧸💬 String matching results - transform of a datetime data fields for a filter.
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
