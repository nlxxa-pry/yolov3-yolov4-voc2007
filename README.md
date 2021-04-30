## YOLOV3 & YOLOV4：You Only Look Once目标检测模型在Pytorch当中的实现
---


## 目录
1. [所需环境](#所需环境)
2. [文件下载](#文件下载)
3. [预测](#预测步骤)
4. [训练](#训练步骤)
5. [评估](#评估步骤)
6. [参考资料](#Reference)


## 所需环境
torch == 1.2.0

## 文件下载
训练所需的yolo_weights.pth可以在百度云下载。   
yolov3:   
链接: https://pan.baidu.com/s/1ncREw6Na9ycZptdxiVMApw   
提取码: appk  
  
yolov4:  
链接：链接: https://pan.baidu.com/s/1WlDNPtGO1pwQbqwKx1gRZA   
提取码: p4sc  
yolo4_weights.pth是coco数据集的权重。  
yolo4_voc_weights.pth是voc数据集的权重。  
  
  
已训练好的模型：  
yolov3：  
链接：https://pan.baidu.com/s/1tREEB_YZs5gJyg3LPeMGEw  
提取码：sa25  
  
yolov4：  
链接：https://pan.baidu.com/s/1BJOgv6jwct92XiPZ9YWYkw  
提取码：w07h  
  
  
VOC数据集下载地址如下：  
VOC2007训练集和验证集    
链接: https://pan.baidu.com/s/1t-4K_TeEolvpshatk9d_Tg 提取码: yylo    

VOC2007测试集   
链接: https://pan.baidu.com/s/1BnMiFwlNwIWG9gsd4jHLig 提取码: dsda   

## 预测
将训练好的模型放入log文件夹（或直接在yolo.py文件中改model path的默认值）  
运行predict.py，输入待检测图片的路径和名称即可使用训练好的模型进行预测  


可输入  
```python
img/street.jpg
```
进行预测 

## 训练
### 训练步骤
1. 本文使用VOC格式进行训练。  
2. 训练前将标签文件放在VOCdevkit文件夹下的VOC2007文件夹下的Annotation中。  
3. 训练前将图片文件放在VOCdevkit文件夹下的VOC2007文件夹下的JPEGImages中。  
4. 在训练前利用voc2yolo3.py文件生成对应的txt。  
5. 再运行根目录下的voc_annotation.py  
6. 此时会生成对应的2007_train.txt，每一行对应其**图片位置**及其**真实框的位置**。   
7. 运行train.py即可开始训练。

### loss曲线
可输入
```python
tensorboard --logdir "log_loss"
```
来获得loss曲线
## 评估
### 评估步骤
1. 本文使用VOC格式进行评估。  
2. 评估前将标签文件放在VOCdevkit文件夹下的VOC2007_test文件夹下的Annotation中。  
3. 评估前将图片文件放在VOCdevkit文件夹下的VOC2007_test文件夹下的JPEGImages中。  
4. 在评估前利用voc2yolo3.py文件生成对应的txt，评估用的txt为VOCdevkit/VOC2007_test/ImageSets/Main/test.txt，需要注意的是，如果整个VOC2007里面的数据集都是用于评估，那么直接将trainval_percent设置成0即可。  
5. 在yolo.py文件里面，在如下部分修改model_path和classes_path使其对应训练好的文件；**model_path对应logs文件夹下面的权值文件，classes_path是model_path对应分的类**。  
6. 运行get_dr_txt.py和get_gt_txt.py，在./input/detection-results和./input/ground-truth文件夹下生成对应的txt。  
7. 运行get_map.py即可开始计算模型的mAP。

### mAP目标检测精度计算
运行
````python
>>> python get_gt_txt.py
>>> python get_dr_txt.py
>>> python get_map.py
````
在result文件夹内测试结果及其可视化  
如mAP AP Precision Recall F1等  
 
（get_map文件克隆自https://github.com/Cartucho/mAP）

## Reference
https://github.com/qqwweee/keras-yolo3  
https://github.com/eriklindernoren/PyTorch-YOLOv3   
https://github.com/BobLiu20/YOLOv3_PyTorch  
https://github.com/bubbliiiing/yolov4-pytorch  
https://github.com/bubbliiiing/yolov3-pytorch  
