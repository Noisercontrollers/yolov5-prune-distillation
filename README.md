## yolov5模型剪枝

yolov5 剪枝, 基于最新v6.0分支,目前支持yolov5所有模型剪枝.

### updates

### BN层剪枝

在VOC2007数据集上实验,训练集为VOC07 trainval, 测试集为VOC07 test. yolov5输入大小为512. AdamW训练100 epoch.

1. 正常训练:

   ```
   python train.py --weights yolov5s.pt --data data/voc.yaml --epochs 100 --imgsz 512 --adam ...
   ```

2. 检测

   ```
   python val.py --weights runs/train/exp*/weights/last.pt --data data/voc.yaml
   ```

3. 稀疏训练
   (1) 正则化BN层γ和β
   ```
   python train_sparity.py --st --sr 0.0002 --weights yolov5s.pt --data data/voc.yaml --epochs 100 --imgsz 512 --adam ...
   ```
   (2) 正则化卷积

4. 剪枝
   (1)正常剪枝
   ```
   python prune.py --percent 0.5 --weights runs/train/exp2/weights/last.pt --data data/voc.yaml --cfg models/yolov5s.yaml
   ```
   (2)通道数为8剪枝
   

5. 微调
   (1)正常微调
   ```
   python finetune.py --weights pruned_model.pt --data data/voc.yaml --epochs 100 --imgsz 512 --adam ...
   ```
   (2)蒸馏微调
6. 检测

   ```
   python val.py --weights runs/train/exp*/weights/last.pt --data data/voc.yaml
   ```


## TD

