# Big Data - T13 - DeepRec
### Flow chart
![pic10](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots/WechatIMG122.jpeg)
### Overview Architecture
![pic11](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots/arche.png)
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

In the root file folder, run the script below to convert the raw data
```
python ./data_utils/netflix_data_convert.py training_set Netflix
```
![picture 1](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots_data%20processing/data%20processing.PNG)

![picture 2](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots_data%20processing/datastats.PNG)

After that, the raw data will be converted into 3 columns with a format of <br>
`CustomerID,MovieID, Rating`

### Model and data test 
For test the autoencoder model, run the script to test the autoencoder for data and layers
```
python -m unittest test/data_layer_tests.py
```
![pic3](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots_data%20processing/test%20for%20data%20layer.png)
```
python -m unittest test/test_model.py
```
![5](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots_data%20processing/test%20models%202.png)<br>
![6](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots_data%20processing/test%20models%20screen%20shot3.png)

![p7](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots/running.PNG)
![picture 8](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots_data%20processing/3Mresult.PNG)
### Result
![finalresult](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots/finalresult.png)