This is a python3 example showing how to build a custom dataset for abcnet training. The example image and annotation are from CTW1500 dataset (https://github.com/Yuliang-Liu/Curve-Text-Detector/tree/master/data)

Step one: Given polygonal annotation, generating bezier curve annotation.
    python Bezier_generator2.py

Step two: Given bezier curve annotation, generating coco-like annotation format for training abcnet.
    python generate_abcnet_json.py ./ train 0

此数据集为任意文本形状的数据集，图片总共有1000张train和500张test。每张图片都由自己的注释txt，下图为1001.jpg图片的注释文件1001.txt，每行包含32个数字，注释一个文本框的位子，有多少行，代表这张图片由多少个文本框。

每行的前4个数字为弯曲文本在整张图上的矩形框坐标值，剩下的28个值为14个点，为相对于矩形框左上角得误差补偿即为与左上角坐标所形成的差值，形成封闭的弯曲文本框。其计算方式可以简单的理解为：

1.将前4个坐标值的矩形框从原图中截取出来（左上右下4个点）

2.在截取之后的图中取14个点的坐标值