# cmpe-255-bonuswork-1

### Recorded operation scenario: https://www.youtube.com/watch?v=7Jykk8jT4u8
## MNIST dataset
For the training of various image processing algorithms, a huge database of handwritten numbers called the \textbf{MNIST database} (Modified National Institute of Standards and Technology database) is frequently employed. The machine learning industry makes extensive use of the database for both training and testing. The samples from the original NIST datasets were "re-mixed" to make it. Since American Census Bureau employees made up the training dataset for NIST, and American high school students made up the testing dataset, the developers concluded that machine learning experiments would not be well-suited to the dataset. The black and white photos from NIST were also anti-aliased, which added grayscale levels, then normalized to fit within a 28x28 pixel grid cell. There are 10,000 testing photos and \textbf{60,000 training images} in the MNIST database.
<br>
<br>
<img src="https://user-images.githubusercontent.com/87613567/202936857-1f6553e5-4e4c-427c-aaa1-aa9f46ca797d.png" width="500" height="300">
<br>
## Prediction using TorchServe
TorchServe is an open-source model serving framework for PyTorch that makes it simple to deploy trained PyTorch models at scale with high performance without having to build special code. With robust TorchServe capabilities including multi-model serving, model versioning for A/B testing, analytics for monitoring, and RESTful APIs for application integration.
<br>
Torchserve’s main purpose is to serve models via http REST APIs.
<br>
<br>
<img src="https://user-images.githubusercontent.com/87613567/202936815-afc9fcd1-2270-44a2-a791-dfb21811e325.png" width="800" height="300">
<br>
Fig 1.TorchServe low level architecture
<br>
## Deployment via REST API (Python Flask)}
Python-based Flask is a compact web server. You can use it to conveniently build up a web API for predictions from your trained PyTorch model, either for usage directly or as a web service within a bigger system.
<br>
When a user uploads several handwritten number photos using my HTML web app, the images are saved in the static subdirectory "UPLOADS" and delivered to the TorchServer, which is operating on port.
<br>
<img src="https://user-images.githubusercontent.com/87613567/202936993-efd7a2ca-e886-4e7c-be9c-38438d4bfc05.png" width="800" height="230">
<br>
Fig 2. Internal flow
<br>
## Steps to run the app:
### 1) Create a Model Archive
``` torch-model-archiver --model-name mnist --version 1.0 --model-file model.py --serialized-file model.pt --handler handler.py ```

### 2) Start Torch Server on Port 8080, 8081
8080 - Management <br/>
8081 - Inference

``` torchserve --start --model-store model_store --models mnist=mnist.mar```

![t1](https://user-images.githubusercontent.com/87613567/202937166-814d2e5e-ab63-49f1-ac20-5af78e1dc193.png)
<br>
### 3) Start Flask app on port 5000 

``` python application/app.py ``` <br>
``` http://127.0.0.1:5000/ ```

![t2](https://user-images.githubusercontent.com/87613567/202937404-2b39350d-cf2c-44c8-a0d8-1c4a1f2a34fb.png)

### 4) Flask app running on port 5000
![t3](https://user-images.githubusercontent.com/87613567/202937451-d8fc23d9-4359-4c74-9fea-4f79f8a3715f.png)

### 5) Upload multiple handwritten number images 
![t4](https://user-images.githubusercontent.com/87613567/202937503-50591fed-206e-4b45-b4a7-065aaebf3bb7.png)


### 6) MNIST prediction 
![t5](https://user-images.githubusercontent.com/87613567/202938615-a028a715-ed9d-43bc-a8b5-cc5746807d75.png)

### 7) Stop TorceServe 
![t6](https://user-images.githubusercontent.com/87613567/202938546-0de4e250-f5fe-4ed2-bcd6-8271bce997f2.png)

## References:
1. https://pytorch.org/serve/ 
2. https://flask.palletsprojects.com/en/2.2.x/<br />
3.https://blog.devgenius.io/get-started-with-multiple-files-upload-using-flask-e8a2f5402e20
