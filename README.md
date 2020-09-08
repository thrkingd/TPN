# TPN

1. 训练入口:train.py,测试入口：eval.py
2. 预训练模型：在kinetics上训练的tsn版本的resnet50
  下载地址：'https://paddlemodels.bj.bcebos.com/video_classification/ResNet50_pretrained.tar.gz'
3. 网络配置参数：采用论文中r50f8s8的网络配置
4. 训练参数：lr=0.01，batchsize=128
5. 图像预处理:首先将视频短边缩放到256，然后随机裁剪224×224区域进行训练，使用随机翻转的增强方式
6. 验证设置：与训练类似，仅采样一个clip采用中心裁剪的方式进行验证，segnum=1，验证acc=0.57
7. 测试：采用论文中的方法，先将视频帧短边缩放到256，然后使用3-crop的方法裁剪3个256×256的patch覆盖长边，每段视频均匀采样10 segnum，即一段视频产生30个样本，将30个样本的预测值进行平均作为视频的预测值，测试记录见./log/eval.txt，acc1=0.63
8. 训练、验证记录：./log/trainer-0_xxxx文件夹下的文件，后缀表示训练日期，前后共训练了11个epoch
9. 训练后的模型参数文件存储在checkpoints文件夹下面，由于文件太大，分割成若干份上传的，使用时先合并再使用。