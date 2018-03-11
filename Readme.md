# Big Data - T13 - DeepRec
### Dataset
[Netflix Prize open competition dataset](https://www.kaggle.com/netflix-inc/netflix-prize-data)<br>
<br>
We mainly used the file `training_set.tar` in the raw dataset. It is a tar of a directory containing 17,770 files, one per movie. The first line of each file contains the movie id followed by a colon. Each subsequent line in the file corresponds to a rating from a customer and its date in the following format:

`CustomerID,Rating,Date`

`MovieIDs` range from 1 to 17,770 sequentially.<br>
`CustomerIDs` range from 1 to 2,649,429, with gaps. There are 480,189 users.<br>
`Ratings` are on a five star (integral) scale from 1 to 5.<br>
`Dates` have the format YYYY-MM-DD.<br>

+ **Data preprocess** <br>
Put the raw data under the root file folder, and then
```
tar -xvf nf_prize_dataset.tar.gz
tar -xf download/training_set.tar
```

We mainly divided movie rating data into three sets: `train set`, `valid set` and `test set`, according to the dates of the ratings. In each set, files have three columns structure: `CustomerID`,`MovieID`,`Rating`.
