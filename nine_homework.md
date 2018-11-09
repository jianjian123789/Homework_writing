# 3 记录过程
## 1. 标注数据
使用labelimg软件标注
## 2. 生成tfrecord格式数据
将标注后的数据整理成如下类似VOC格式的数据形式：
![image.png](http://note.youdao.com/yws/res/17069/WEBRESOURCE25c42591b9f353c79443a4264954520b)
```
data:
    quiz8_data:
        + images：  
            原始图片
        + annocations:
            + xmls
                *.xml标注文件
        labels_items.txt
        + test_images:
            test.jpg
            labels_items.txt
models:
    ssd_mobilenet_v1_pets_nine.config
        
```

然后运行以下命令： 
```
# From tensorflow/models/research/ 
(env2) wj@wj-G4:~/models/research$  
python object_detection/dataset_tools/nine_work_to_tfrecord.py    
--label_map_path=object_detection/data/quiz-w8-data/labels_items.pbtxt  
--data_dir=./object_detection/data/quiz-w8-data/  
--output_dir=`pwd`

其中nine_work_to_record.py具体内容参考github第九周作业或者本地02-CSDN/nine_weeks
这个脚本文件是参考/object_detection/dataset_tools/create_pet_tf_record.py编写。

```
![image.png](http://note.youdao.com/yws/res/17063/WEBRESOURCEb16ae597c839cb82fc988047511d9319)

## 3. config配置/运行/验证
配置文件我们选择models/research/object_detection/samples/configs/ssd_mobilenet_v1_pets.config   
```
具体代码配置位置在02-CSDN/nine_weeks/to_tfrecord.py
```



```
# 这个是我们在最新的models的API中运行的命令：  
然后在/research/目下运行代码：  
PIPELINE_CONFIG_PATH=/home/wj/models/research/object_detection/models/ssd_mobilenet_v1_pets_nine.config
MODEL_DIR=/home/wj/models/research/object_detection/models/train_nine
NUM_TRAIN_STEPS=5000
SAMPLE_1_OF_N_EVAL_EXAMPLES=1
#python object_detection/model_main.py \
python object_detection/model_main.py \
    --pipeline_config_path=${PIPELINE_CONFIG_PATH} \
    --model_dir=${MODEL_DIR} \
    --num_train_steps=${NUM_TRAIN_STEPS} \
    --sample_1_of_n_eval_examples=$SAMPLE_1_OF_N_EVAL_EXAMPLES \
    --alsologtostderr


# 这个是我们直接在modelsr1.5的API上进行运行的命令：
# 本地运行训练
(env1) wj@wj-G4:~/models/research$ 
python ./object_detection/legacy/eval.py --logtostderr  --train_dir=/home/wj/models/research/object_detection/models/train_nine/ --pipeline_config_path=/home/wj/models/research/object_detection/models/ssd_mobilenet_v1_pets_nine.config

# 本地运行验证，注意这里的checkpoint就是训练时候的train_dir,验证的结果放在eval_dir，可以通过tensorboard看
(env1) wj@wj-G4:~/models/research$ 
python ./object_detection/legacy/eval.py --logtostderr  --checkpoint_dir=/home/wj/models/research/object_detection/models/train_nine/ --eval_dir=/home/wj/models/research/object_detection/models/eval_nine/ --pipeline_config_path=/home/wj/models/research/object_detection/models/ssd_mobilenet_v1_pets_nine.config


```
![image.png](http://note.youdao.com/yws/res/17129/WEBRESOURCEd7939cac67390dfd22e594493f890967)



## 4. 查看/冻结导出模型
```
# 查看模型使用tensorboard：  
#(env1) wj@wj-G4:~/models/research/
tensorboard --logdir=~/models/research/object_detection/models/train_nine/



# 导出训练好的模型
# From tensorflow/models/research/
#(env1) wj@wj-G4:~/models/research/
INPUT_TYPE=image_tensor
#需要进行更改为自己的配置路径
PIPELINE_CONFIG_PATH=/home/wj/models/research/object_detection/models/ssd_mobilenet_v1_pets_nine.config
#需要更改为我们刚刚预训练的checkpoint
TRAINED_CKPT_PREFIX=/home/wj/models/research/object_detection/models/train_nine/model.ckpt-1743
#导出路径的位置文件夹
EXPORT_DIR=/home/wj/models/research/object_detection/models/export_nine/exported_graphs
python object_detection/export_inference_graph.py \
    --input_type=${INPUT_TYPE} \
    --pipeline_config_path=${PIPELINE_CONFIG_PATH} \
    --trained_checkpoint_prefix=${TRAINED_CKPT_PREFIX} \
    --output_directory=${EXPORT_DIR}
```
运行导出模型之后的结果如下：  
![image.png](http://note.youdao.com/yws/res/17145/WEBRESOURCE3f12e223f061aa5269b7c5d1c389ca04)

## 5. 测试：运行导出模型
```
# 用导出的模型运行inference，详情参考代码
(env1) wj@wj-G4:~/models/research/object_detection$
python ./inference.py --output_dir=/home/wj/models/research/object_detection/models/export_nine/  --dataset_dir=/home/wj/models/research/object_detection/data/quiz-w8-data/test_images/

# output_dir:就是我们刚刚导出的文件夹目录。  
# dataset_dir:就是我们测试的一张图片所在所在目录。  

```
![image.png](http://note.youdao.com/yws/res/17159/WEBRESOURCE10369252dacebdfbcf00e52ed6700d31)
![image.png](http://note.youdao.com/yws/res/17205/WEBRESOURCEbac2928bbda6787917469f5c6523597c)

## 6. 出现的问题汇总

---
1.运行程序时：  
```
先进行install安装操作
```
---
2.运行训练程序时：  
```
# C:\Users\nicho\Documents\01_Machine_Learning\00_Lynda.com\Ex_Files_TensorFlow\models\research\object_detection> 
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/ssd_mobilenet_v1_pets.config

出现如下错误：  
 File "C:\Users\nicho\Anaconda3\envs\tensorflow\lib\site-packages\tensorflow\python\ops\array_ops.py", line 1054, in unstack
    (axis, -value_shape.ndims, value_shape.ndims))
ValueError: axis = 0 not in [0, 0)


解决办法：修改配置文件操作
problem solved. In your pipeline.config make
```
[配置文件修改loss参考](https://stackoverflow.com/questions/48847365/tensorflow-object-detection-api-training-error)

---

```
# C:\Users\nicho\Documents\01_Machine_Learning\00_Lynda.com\Ex_Files_TensorFlow\models\research\object_detection> 
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/ssd_mobilenet_v1_pets.config



出现如下错误：  
  File "/home/vaishnav/cv/lib/python3.5/site-packages/tensorflow/python/framework/errors_impl.py", line 473, in __exit__
    c_api.TF_GetCode(self.status.status))
tensorflow.python.framework.errors_impl.NotFoundError: ; No such file or directory


解决办法：命令行中--前面要有空格
```
---

仍然想要使用老版本的train.py的方法，这样便于在终端显示出step的loss

```
这个是由于版本问题
```
[参考文档](https://www.cnblogs.com/zongfa/p/9663649.html)

---
3.运行测试程序的时候：
```
将02-CSDN/nine_weeks/inferences.py放到脚本放到models/research/objection_detection/目录下
```

---
