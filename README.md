# Machine Learning End Of Year Project Repport

Arnaud Martin

I know you probably have read too much paper already for a Christmas vacation so don't hesitate to skip to the parts **summary evaluate, improve, argument**. They will provide you with all you need to grade this work. The paper in itself 

[TOC]

## Dataset overview

I choosed to work with the image (colorectal-histology) dataset. The dataset was released with a paper (Kather, 2016) [1]. It is composed of 5,000 images of colon divided in eight classes.  The classes are:

1. tumor epithelium, 
2. simple stroma
3. complex stroma
4. immune cells
5. debris and mucus
6. mucosal gland
7. adipose tissue
8. background

## Author's work overview

 Authors converted images to grey scale. And developed a set of problem specific features divided in 6 broad categories that we won't detail here. Then they used four classifiers 1-NN, ensmble tree, linSVM and rbfSVM. And they defined two types of of problems. The first is multiclass problem where they try to predict the label of the image. The second is the conventional problem where they try to predictif if the patient has a cancer or not.

Multiplying feature sets, classifiers and problems there are 48 models authors compare using error rates. Error rates varies from 4% to 50%.

## Problem Definition

The point of the project is to showcase how to improve (& build) a predictive model using these images.

In my non-expert understanding, stroma (simple or complex) [2],  immune cells [3], debris and mucus [4], mucosal glands [5],  adipose tissue [6] and background are not conditions. The only class that require special attention is the first one [7].  

I want to build (a little bit) on the authors work. I assume in a real scenario with such an application a doctor will confirm any positive. So I think error rate is not the most important metric for the patient. So I will try to make a model that prioritize not missing tumor prediction even at the expanse of predicting other classes as tumor.

My plan is to first build a model that the authors did not explore a CNN. Then to compare it's error rate to the authors models. Then depending on the time I have I will either try to improve it and compare it's recall to my model or try a model made by the authors and compare it's recall to my model. 

## Baseline model description

I choosed to go for a CNN base line model because it was the one I would implement the fastest. At first I choosed not to go throught any preprocessing as I had no idea if it would have any impact for the work and since I did not had a base line model I wouldn't be able to compare the impact of the preprocessing





## Summary on skill evaluate

* I decided to focus on the tumor/not tumor problem because it is the most important to an hypothetical patient
* I used recall as a metric. Ethically a false negative could mean a patient's death while a false positive would likely be caught on by an other doctor in the healing process. False negative is the enemy in this problem.
* I used error rate as a metric as it is the metric used by the authors of the original dataset and I compared my models to theirs. (I realy used accuracy and Error rate = 1 - Accuracy)
* Just to be nerdy and try it out I made some ROC curves.

## Summary on skill improve 

| Model version         | Argument                                                     | metrics                                     | explain                                                      |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------- | ------------------------------------------------------------ |
| Author's              | Not mine                                                     | recall : ???<br />ER : 4.3~21.7             | I think recall would be a more interesting metric.           |
| Baseline              | - Made fast (in developement time)<br />-No Preprocessing<br />-CNN from flower TP<br />- 5 epochs | Recall : 0<br />ER : 23%                    | The models always predict healthy. Probably because most example are healthy. |
| v1<br />Data augment° | -Same as base line<br />-Data augmentation (rotation only to not trim the tumor: I have no medical knowledge) for tumor examples to 50/50 healthy/unhealthy ratio | Recall : 0.9%<br />ER : 99.1 (0.9=9samples) | - Recall is not 0 but I expected at least 50%<br />- Model output is always around 0.45 <br />-To me it seem the model is mostly random. Maybe the task is too complex for the model<br />-When model says positive the person is really positive |
| v2                    | - Same as v1<br />-Simplified input by going grey scale<br />-Complexified model by adding depth and width | ER:100%<br />Recall:0                       | - At this point I think I have a bug<br />-Maybe the shuffle doesn't < |
| v3   | - Implemented manually train_test_split and shuffle   | ER:43%<br />Recall:0  | I notice accuracy does not update through epochs and find it could be due to a bad learning rate selection [8] |
| v4   | - I search for a good learning rate using grid search | ER:~45%<br />Recall:0 | For all tested learning rates (1 to 0.001) Recall always stayed at 0. |





## Bibliography & Sources

[1] - Kather, J., Weis, CA., Bianconi, F. *et al.* Multi-class texture analysis in colorectal cancer histology. Sci Rep **6**, 27988 (2016). https://doi.org/10.1038/srep27988

[2] - https://en.wikipedia.org/wiki/Stroma_(tissue)

[3] - https://en.wikipedia.org/wiki/Nonspecific_immune_cell

[4] - https://www.frontiersin.org/articles/10.3389/fcimb.2020.00248/full

[5] - https://en.wikipedia.org/wiki/Mucous_gland

[6] - https://en.wikipedia.org/wiki/Adipose_tissue

[7] - https://en.wikipedia.org/wiki/Epithelioma
