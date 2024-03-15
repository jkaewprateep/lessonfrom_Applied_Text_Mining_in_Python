# University of Michigan - Applied Text Mining in Python - notes
University of Michigan - Applied Text Mining in Python

## This note we aim to study text mining and I found interesting of text mining applications from the course examples including medical records and social media as sources.

## 🧸💬 Sample of input data
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

## 🧸💬 String matching method
```
for idx, item in enumerate(doc) :
    item = item.strip();
    match_string_one = r"((?:\d{1,2})(?:(?:\/|-)\d{1,2})(?:(?:\/|-)\d{2,4}))";
    answer_one = re.search(match_string_one, item);
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
