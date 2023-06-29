# Hijab_Detection
### Description
The hijab object detection is an object detection task that detects whether people are wearing hijabs or masks in pictures or videos. This repository includes a demo for building a hijab or face mask detector using YOLO v5 model.

### Dataset
The model was trained on dataset which contains 377 hijab or mask images belonging to 4 classes. The classes are defined as follows:<br>
* burqz(burqa)
* chador
* mask
* niqab

→ This model will be further trained on a dataset that contains about 2,000 hijab or mask images belonging to 4 classes.<br>

### Data Collection
The data collection for this project was initially done through Google search, and then we labeled the collected images.<br>
The 2,000 images will be trained by applying a pseudo labeling technique.<br>

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
TBU

### Test Result
TBU
