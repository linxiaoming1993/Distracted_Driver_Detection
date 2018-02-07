# Distracted_Driver_Detection
开车状态识别

# 参考
- https://github.com/ypwhs/DogBreed_gluon
- https://www.kaggle.com/c/state-farm-distracted-driver-detection/discussion/20747
- http://zh.gluon.ai/chapter_convolutional-neural-networks/densenet-gluon.html

# 驾驶状态分类
## 环境说明
- python3 
- mxnet 1.0.0

## 数据说明
数量来源[https://www.kaggle.com/c/state-farm-distracted-driver-detection/data](https://www.kaggle.com/c/state-farm-distracted-driver-detection/data),下载并解压缩。

[train](train)、[test](test)中存储了原始的图片数据，其中[train](train)中的数据按照类别分类存好了。类别说明如下：
- c0: safe driving
- c1: texting - right
- c2: talking on the phone - right
- c3: texting - left
- c4: talking on the phone - left
- c5: operating the radio
- c6: drinking
- c7: reaching behind
- c8: hair and makeup
- c9: talking to passenger

[sample_submission](sample_submission.csv)存储了test数据的预测样例。

[driver_imgs_list.csv](driver_imgs_list.csv.csv)存储了训练集中每张图片属于的人的标签

## 数据预处理
- 按照[data_split.ipynb](data_split.ipynb)做数据划分。
- 生成rec和lst文件。得到的结果存储在[train_lst](train_lst)和[test_lst](test_lst)中。

# 方法一
预训练模型提取特征，然后训练全连接网络用于分类。
### 特征提取
[features_extraction.ipynb](features_extraction.ipynb)用于特征的提取。使用预训练好的模型提取图片的特征，并将特征存储在[features](features)中。

### 分类模型训练
[classification_train.ipynb](classification_train.ipynb)选择合适的预训练模型，用于训练分类模型。并融合多个预训练模型提取的特征用于训练分类模型，并将模型结果存储在[model](model)。

### 预测
[predict.ipynb](predict.ipynb)预测[test](test)中图片的类别，并对照[sample_submission](sample_submission.csv)的格式存储好。将结果保存在[predict](predict)中。

# 方法二
[classification_method2.ipynb](classification_method2.ipynb)预训练好的网络，保留特征提取层（卷积层），最后添加分类层。然后重新训练网络。模型结果存储在[model](model)。预测结果保存在[predict](predict)中。
