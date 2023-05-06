yolov5_onnx2caffe

参考工程：

[caffe](https://github.com/Wulingtian/yolov5_caffe)

[caffe docker](https://github.com/BVLC/caffe/tree/master/docker)

[onnx2caffe](https://github.com/Wulingtian/yolov5_onnx2caffe)

创建docker

```
$ docker build -t caffe-yolov5-chliu_v1:cpu build_docker/
$ docker run -it  --name chliu_caffe_yolov5_build_v1 caffe-yolov5-chliu_v1:cpu /bin/bash
```

上传docker

```
$ docker login   ### docker 账号chliu4890  密码 Vs4***5.
$ docker images
$ docker tag caffe-yolov5-chliu_v1:cpu chliu4890/caffe-yolov5-chliu
$ docker push chliu4890/caffe-yolov5-chliu
```

使用docker

```
$ docker pull chliu4890/caffe-yolov5-chliu:latest
$ docker run -it  --name chliu_caffe_yolov5_build_v1 chliu4890/caffe-yolov5-chliu:latest /bin/bash
或
$ docker run -it  -v /diskd/liuchang298/liu_file/:/workspace --name chliu_caffe_yolov5_build_v1 chliu4890/caffe-yolov5-chliu:latest /bin/bash
```



转换模型

```
$ docker start chliu_caffe_yolov5_build_v1
$ docker exec -it chliu_caffe_yolov5_build_v1 /bin/bash
$ cd /root/yolov5_onnx2caffe
$ python convertCaffe.py  # 使用时需要更改模型路径
```

