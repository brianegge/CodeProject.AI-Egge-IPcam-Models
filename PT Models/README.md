I trained these models on my Ubuntu 22.04 server with a Nvidia 3080. The steps are as follows:

```
mkdir yolov5
cd yolov5
git clone https://github.com/ultralytics/yolov5
python -m venv .
source bin/activate
pip install -r yolov5/requirements.txt

curl -L "https://app.roboflow.com/ds/XXXXXX" > roboflow.zip; unzip roboflow.zip; rm roboflow.zip
python yolov5/train.py --data data.yaml --weights yolov5s.pt --imgsz 608 --epochs 300
sudo cp yolov5/runs/train/exp/weights/best.pt /usr/bin/codeproject.ai-server-2.5.1/modules/ObjectDetectionYOLOv5-6.2/custom-models/egge.pt
```

Then I `sudo systemctl restart codeproject.ai-server.service`

Afterwhich, I could test in the CodeProject AI explorer:
![CodeProject Explorer](codeproject-package.png?raw=true)

