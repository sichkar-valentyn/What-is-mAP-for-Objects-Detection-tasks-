# What is mAP for Objects Detection tasks?
mAP as a main metric for Objects Detection

### Related Course where mAP is used
**Training YOLO v3 for Objects Detection with Custom Data.** *Build your own detector by labelling, training and testing on image, video and in real time with camera.* Available here: [https://www.udemy.com/course/training-yolo-v3-for-objects-detection-with-custom-data/](https://www.udemy.com/course/training-yolo-v3-for-objects-detection-with-custom-data/)

![Detections on Images](https://github.com/sichkar-valentyn/YOLO-v3-Objects-Detection-with-Custom-Data/blob/master/images/slides_detections_2.gif "YOLO v3 Objects Detections on Images")


### Content
* [Definition](#definition)
* [Important terminology](#important-terminology)
* [Calculating Average Precision (AP)](#average-precision)

<br/>

### <a id="definition">Definition</a>
**mAP (mean average precision)** is a metric used to evaluate accuracy, in our case, for *Objects Detection* tasks.
In general, to calculate *mAP* for a custom model that is trained for *Objects Detection tasks*, firstly, *Average Precision* is calculated for every class in the custom model. Then, mean of these calculated *Average Precisions* across all classes gives *mAP*.
*Pay attention!* Some papers use Average Precision and mAP interchangeably.

<br/>

### <a id="important-terminology">Important terminology</a>
Understanding the calculation process of *Average Precision* needs to update knowledge of definitions for used parameters.

- [x] **Threshold** is used to identify whether prediction of *Bounding Box (BB)* can be considered as *True* or *False*. Usually threshold is set to one of the following: **50%, 75%, 95%**.

- [x] **Intersection Over Union (IoU)** is a measure that is used to evaluate **overlap** between two **Bounding Boxes (BB)**. *IoU* shows how much predicted *BB* overlaps with so called **Ground Truth BB** (the one that has real object inside). Comparing *IoU* with threshold it is possible to define whether predicted *BB* is **True Positive** (valid in other words) or **False Positive** (not valid).
**IoU** is calculated by overlapping area between *predicted BB* and *Ground Truth BB* divided by union area of two *BB* as shown on the Figure below.
![Intersection Over Union (IoU)](https://github.com/sichkar-valentyn/What-is-mAP-for-Objects-Detection-tasks-/blob/master/images/iou.png "Intersection Over Union (IoU)")

- [x] **True Positive (TP)** is a number of BB with correct predictions, IoU ≥ threshold
- [x] **False Positive (FP)** is a number of BB with wrong predictions, IoU < threshold
- [x] **False Negative (FN)** is a number of Ground Truth BB that are not detected
- [x] **True Negative (TN)** is a number of BB that are correctly not predicted (as many as possible within an image but not overlap any Ground Truth BB); this parameter is not used for calculating metrics

- [x] **Precision** represents percentage of correct *positive predictions of BB* (how accurate are predicted BB) and shows an ability of the trained model to detect relevant objects. *Precision* is calculated as following:
![Precision](https://github.com/sichkar-valentyn/What-is-mAP-for-Objects-Detection-tasks-/blob/master/images/precision.png "Precision")

- [x] **Recall** represents percentage of *True Positive predictions of BB* among all relevant *Ground Truth BB* and shows an ability of the trained model to detect all *Ground Truth BB*. *Recall* is calculated as following:
![Recall](https://github.com/sichkar-valentyn/What-is-mAP-for-Objects-Detection-tasks-/blob/master/images/recall.png "Precision")

- [x] **Precision and Recall curve** represents performance of the trained model by plotting a curve of Precisions values against Recalls values and form a kind of zig-zag graph as shown on Figure below.
![Precision and Recall curve](https://github.com/sichkar-valentyn/What-is-mAP-for-Objects-Detection-tasks-/blob/master/images/precision_recall_curve.png "Precision and Recall curve")

In order to plot *Precision and Recall curve*, it is needed to collect detected BB by their confidences in *descending order*. Then, calculate *Precision* and *Recall* for every detected BB as it is shown in Table below. In current example, threshold is set to 50% saying that predicted BB is correct if *IoU ≥ 0.5*. Total number of correct predictions TP = 5 and total number of wrong predictions FP = 5.

BB | Confidence | TP or FP | Precision | Recall
-- | -- | -- | -- | --
1 | 96% | TP | 1/1 = 1 | 1/5 = 0.2
2 | 94% | FP | 1/2 = 0.5 | 1/5 = 0.2
3 | 90% | TP | 2/3 = 0.67 | 2/5 = 0.4
4 | 89% | TP | 3/4 = 0.75 | 3/5 = 0.6
5 | 81% | FP | 3/5 = 0.6 | 3/5 = 0.6
6 | 75% | TP | 4/6 = 0.67 | 4/5 = 0.8
7 | 63% | TP | 5/7 = 0.71 | 5/5 = 1
8 | 59% | FP | 5/8 = 0.62 | 5/5 = 1
9 | 54% | FP | 5/9 = 0.56 | 5/5 = 1
10 | 51% | FP | 5/10 = 0.5 | 5/5 = 1

<br/>

### <a id="average-precision">Calculating Average Precision (AP)</a>
*AP* is calculated by considering area under **Interpolated Precision and Recall curve**. Firstly, *Recall* values are divided into *11 points* as following: *[0, 0.1, 0,2 … 1]* as shown on Figure below.
![Interpolated Precision and Recall curve](https://github.com/sichkar-valentyn/What-is-mAP-for-Objects-Detection-tasks-/blob/master/images/ap_curve.png "Interpolated Precision and Recall curve")

Then, average of maximum precision values is computed for these *11 Recall points*.
![Average](https://github.com/sichkar-valentyn/What-is-mAP-for-Objects-Detection-tasks-/blob/master/images/ap.png "Average")

From our example, *AP* will be calculated as following:
<br/>**AP = (1/11) * (1+1+1+0.75+0.75+0.75+0.75+0.71+0.71+0.71+0.71) = 0.81**

<br/>

### MIT License
### Copyright (c) 2020 Valentyn N Sichkar
### github.com/sichkar-valentyn
