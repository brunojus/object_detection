## Introduction
 This repo contains object_detection.py which is able to perform the following task -
 - Object detection from live video frame, in any video file or in a image
 - Counting the number of objects in a frame
 - Measuring the distance of object using IPM
 - Inferece on Multiple Camera feed at a time
 
For object detection YOLO-V3 has been used which is able to detect 80 different objects. Some of those are-
- person
- car
- bus
- traffic sign
- truck
- bycicle


### User Instruction
To execute object_dection.py you require Python version > 3.5 (depends if you are using gpu or not) and have to install the following libraries.

### Instalation
``` python
    $ pip install -r requirements.txt
         or
    $ pip install opencv-python
    $ pip install numpy
    $ pip install pandas
    $ pip install matplotlib
    $ pip install Pillow
```
<hr>

#### For the installation of torch using "pip" 
``` python
    $ pip3 install torch===1.2.0 torchvision===0.4.0 -f https://download.pytorch.org/whl/torch_stable.html
```
or please follow the instructions from [Pytorch](https://pytorch.org/)

You need to clone the repository using gitbash (if gitbash is already installed) or you can download the zip file.

After unzipping the project, there are two ways to run this. If want to see your output in your browser execute the "app.py" script or else run "object_detection.py" to execute it locally.


If you want to run object detection and distance measurement on a video file just write the name of the video file to variable <b>id</b> in either "app.py" or "object_detection.py" or if you want to run it on your webcam just put 0 in <b>id</b>.

However, if you want to run the infeence on a feed of <b>IP Camera </b>, use the following convention while assigning it to the variable <b>"id"</b>
``` python
    "rtsp://assigned_name_of_the_camera:assigned_password@camer_ip/"
```

You can check the performance on differet weights of YOLO which I have added on google drive and also available in [YOLO](https://pjreddie.com/darknet/yolo/?style=centerme)

For multiple camera support you need to add few codes as follows in app.py-

``` python
   def simulate(camera):
       while True:
           frame = camera.main()
           if frame != "":
               yield (b'--frame\r\n'
                   b'Content-Type: image/jpeg\r\n\r\n' + frame + b'\r\n\r\n')

   @app.route('/video_simulate')
   def video_simulate():
       id = 0
       return Response(gen(ObjectDetection(id)), mimetype='multipart/x-mixed-replace; boundary=frame')
```

Depending on how many feed you need, you have to add the two methods in "app.py" with different names and add a section in index.html.

``` html
<div class="column is-narrow">
        <div class="box" style="width: 500px;">
            <p class="title is-5">Camera - 01</p>
            <hr>
            <img id="bg" width=640px height=360px src="{{ url_for('video_simulate') }}">
            <hr>

        </div>
    </div>
    <hr>
```
#### Note: 
You have to use git-lfs to download the yolov3.weight file. However you can also download it from here [YOLOv3 @ Google-Drive](https://drive.google.com/drive/folders/1nN49gRqt5HvuMptfc0wRVcuLwiNmMD6u?usp=sharing)
<hr>

