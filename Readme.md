# Big Data - T13 - DeepRec
## Flow chart
![pic10](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots/WechatIMG122.jpeg)
## Overview Architecture
![pic11](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots/arche.png)
## Dataset
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

In the root file folder, run the script below to process the original Netflix dataset and output the basic statistics of number of ratings and users.
```
python ./data_utils/dataprocessing.py training_set Netflix
```
![picture 2](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots_data%20processing/datastats.PNG)

After that, the raw data will be converted into 3 columns with a format of <br>
`CustomerID,MovieID, Rating`

+ **Model and data test 
For test the autoencoder model, run the script to test whether the autoencoder for data and layers is working smoothly.
```
python -m unittest test/data_layer_tests.py
```
```
python -m unittest test/test_model.py
```

### Train
```
python train.py --gpu_ids 0 --path_to_train_data Netflix/N3M_TRAIN --path_to_eval_data Netflix/N3M_VALID --hidden_layers 128,256,256 --non_linearity_type selu --batch_size 128 --logdir model_save --drop_prob 0.8 --optimizer momentum --lr 0.005 --weight_decay 0 --aug_step 1 --noise_prob 0 --num_epochs 100 --summary_frequency 1000

```
### Evaluate
```
python evaluate.py --path_to_train_data Netflix/N3M_TRAIN --path_to_eval_data Netflix/N3M_TEST --hidden_layers 128,256,256 --non_linearity_type selu --save_path model_save/model.epoch_99 --drop_prob 0.8 --predictions_path preds.txt

```

### Result
![finalresult](https://github.com/jeness/BigData_T13_DeepRec/raw/master/screenshots/finalresult.png)