# Hijab_Detection
### Description
The hijab object detection is an object detection task that detects whether people are wearing hijabs or masks in pictures or videos. This repository includes a demo for building a hijab or face mask detector using YOLO v5 model.

### Description ipynb files
* Pseudo_Labeling.ipynb<br>
  Data Labeling using Yolov5<br>
  Through this file, You can learn how to label new data through existing models.<br>
* Data_Processing.ipynb<br>
  The process about preprocessing dataset<br>
  Through this file, you can remove duplicate image data.(the file path needs to be modified)<br>
* Object_Detection_with_YOLO_v5_hijab.ipynb<br>
  An overview file for model training<br>
  Through this file, You can see the process by which we have learned the model, verified it, and performed predictions.<br>
  (You don't need to modify the code to perform it.)
* Inference_Dataset.ipynb<br>
  Detecting hijab related object using collected dataset<br>
  Through this file, you can see the difference between the results of a model with a small number of data and the results of a model with a large number of data.<br>  

→ This model will be further trained on a dataset that contains about 2,000 hijab or mask images belonging to 4 classes.<br>


# Data
  
### Dataset
The model was trained on dataset which contains 377 hijab or mask images belonging to 4 classes. The classes are defined as follows:<br>
* burqz(burqa)
* chador
* mask
* niqab
  
#### File Structure
```bash
hijab
├── images
│   ├── test-current
|   |   ├── burqz
|   |   ├── chador
|   |   ├── mask
|   |   └── niqab 
│   ├── test-past
|   |   ├── burqz
|   |   ├── chador
|   |   ├── mask
|   |   └── niqab 
│   ├── train
|   |   ├── burqz
|   |   ├── chador
|   |   ├── mask
|   |   └── niqab 
│   └── val
|       ├── burqz
|       ├── chador
|       ├── mask
|       └── niqab 
└── labels
    ├── test
    |   ├── burqz
    |   ├── chador
    |   ├── mask
    |   └── niqab 
    ├── train
    |   ├── burqz
    |   ├── chador
    |   ├── mask
    |   └── niqab 
    └── val
        ├── burqz
        ├── chador
        ├── mask
        └── niqab 
```
### Data Collection
We collected data in a variety of ways.<br>
1. We collected about 800 image data by crawling Google and Bing sites.<br>
#### Data Deduplication 
We maked python code for deduplicating images. you can find python code in "Inference_Dataset.ipynb" file<br>

2. We collected about 200 image data by using chrome extension program(Image Downloader, you can find easily to search chrome market "Image Downloader") <br>
#### Data Labeling
We used DarkLabel(Data Labeling Program operating in a Windows environment)
* You can download DarkLabel in Github (https://github.com/darkpgmr/DarkLabel)<br>
* We Labeled data following this file. => [DarkLabel.pdf](https://github.com/dalabdgw/Hijab_Detection/files/12026408/DarkLabel.pdf) <br>

### Setup
* Clone this repository and install YOLO v5
<pre><code>git clone https://github.com/dalabdgw/Hijab_Detection.git

# install YOLO v5
!git clone https://github.com/ultralytics/yolov5.git
!pip install -r ./yolov5/requirements.txt
</code></pre>

### Training
* --data : yaml file path (yaml file with data set information)
* --weights : Pre-Trained model file path (pt format file), if no value is entered (‘’), initialize and train with a random weight value
* --epochs : epoch size
* --batch : batch size
* --cfg : The model size determined above (saved as a yaml file in the yolov5/models folder)
  * s is the lightest model x is the heaviest model Of course, s has the lowest performance but the highest FPS, and x has the highest performance but the lowest FPS.
<pre><code>python ./yolov5/train.py --img 640 --batch 16 --epochs 50 --data ./dataset/hijab.yaml --cfg ./models/yolov5s.yaml --weights yolov5s.pt --name hijab_yolov5s_results</code></pre>

### Inference
* If training the model was finished, use the following command for inference.
* example
<pre><code>val_img_path = './hijab/images/test/chador/84.jpeg'
!python ./yolov5/detect.py --weights ./yolov5/runs/train/hijab_yolov5s_results/weights/best.pt --source "{val_img_path}"</code></pre>

# Result 
### Training Result

|epochs|50|100|150|365|
|---|---|---|---|---|
|precision|0.93831|0.94186|0.9059|0.95066|
|recall|0.93044|0.87181|0.92202|0.88883|
|mAP_0.5|0.95287|0.94876|0.93225|0.93946|
|mAP_0.5:0.95|0.64209|0.64262|0.62445|0.6287|
|result_img|![image](https://github.com/dalabdgw/Hijab_Detection/assets/135303032/9f2fbb5d-c9c6-488d-b960-be73a99aba1d)|![스크린샷 2023-07-11 182602](https://github.com/dalabdgw/Hijab_Detection/assets/135303032/293d32ae-800f-4e9c-886e-adee47b690b1)|![image](https://github.com/dalabdgw/Hijab_Detection/assets/135303032/0bdd2e2d-fef5-4c1f-9b33-c8c9a53a5f7a)|![image](https://github.com/dalabdgw/Hijab_Detection/assets/135303032/ce9cd7d8-2f42-432a-bc35-a85a1a956c66)|



### Test Result (Tested on models with epochs 50)

|mask|niqab|chador|burqz|
|---|---|---|---|
|![image](https://github.com/dalabdgw/Hijab_Detection/assets/135303032/680d65fc-cf07-4c79-8890-ba6afe5fc3d2)|![image](https://github.com/dalabdgw/Hijab_Detection/assets/135303032/dea1d290-1619-4d12-85cc-c777aaed6598)|![image](https://github.com/dalabdgw/Hijab_Detection/assets/135303032/903bd4c0-405c-42e8-a448-a46aa6f8cc4d)|![image](https://github.com/dalabdgw/Hijab_Detection/assets/135303032/99e0b0d5-747b-4926-a85e-d4e5771bfb4a)|

