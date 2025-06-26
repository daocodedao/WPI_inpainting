# 注释分割与移除 
![image](successful_removal_comparison.png)

利用 [LBAM 图像修复模型](https://github.com/Vious/LBAM_Pytorch)，移除由 [Synthesis in Style](https://github.com/hendraet/synthesis-in-style) 检测到的手写笔迹。

## 环境设置

确保你在 ```/final_application/synthesis_in_style_lightning``` 目录下有 Synthesis in Style Lightning 的文件，
然后再通过 Git 子模块在本地安装。这些文件可以从 [这里](https://github.com/adbu42/synthesis-in-style-lightning/tree/training_loop_to_lighning) 复制。
可以通过 pip 和 requirements.txt 文件安装所需依赖。
或者，你也可以使用 Docker 镜像 "docker://hendraet/synthesis-in-style:cuda-11.1"。
模型权重可以从 [这里](https://drive.google.com/file/d/1O_bImshs5KXloh2Nd05TzmiQIqIlJw0i/view?usp=sharing) 和 [这里](https://drive.google.com/file/d/19daBLbYazgU6q2EaEdHudJqrkWSWYlqf/view?usp=sharing) 下载。

## 文件说明

### fill_handwriting_with_background.py

通过用文档的均值填充手写笔迹区域，从文档中移除手写笔迹。
使用方法：
```
fill_handwriting_with_background.py --input-dir "directory of the documents with handwriting" --output-dir "output directory"
```

### remove_handwriting.py

通过用 LBAM 模型的输出替换手写笔迹区域，从文档中移除手写笔迹。
使用方法：
```
remove_handwriting.py --input-dir "包含手写笔迹文档的目录" --output-dir "输出目录"
```

### get_pnsr_and_ssim.py

输出两个包含文档图像的目录之间的峰值信噪比（PSNR）、结构相似性指数（SSIM）、均方误差（MSE）和 L1 损失。两个目录都应包含图像。
该脚本仅比较两个目录中同名的图像。
真实图像和去除手写笔迹后的图像应具有相同的分辨率和尺寸。
使用方法：
```
get_pnsr_and_ssim.py --ground-truth "包含真实图像的目录" --removed-handwriting "包含修复后图像的目录"
```
