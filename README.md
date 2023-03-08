# Anomaly-Detection

***Kaggle dataset Link and References***
- https://www.kaggle.com/datasets/stephanmatzka/condition-monitoring-dataset-ai4i-2021
- https://www.kaggle.com/datasets/fedesoriano/synchronous-machine-dataset

**Assignment Requirement**

Detect anomaly and alert defects from an unstructured data pool received from current sensors of a 3-phase induction motor at a rate of 10K - 15K instances per second. 

Dataset:
https://drive.google.com/drive/folders/1d70I-XacHhA7i7MsVQa-iFJvp2nTiayA?usp=share_link

the data set contains current readings of a 3-phase AC motor (3.2hp) 
motor current signature analysis and model-based VI analysis to be done to detect anomalies 

Structure/process the data, create condition indicators, create an ML model, and create features to train the model.  The model should learn, and predict future anomalies. 
For other data, you can get data set from kaggle or other online sources as well.

Study on MCSA, model-based VI analysis, and how they're applied to predict machine failure.

How to submit:
Share it on GitHub or GitLab with proper documentation 
1. what you have done - logic
2. how it can be set up and tested in an isolated system (share deployable/dockerized code)
3. create an anomaly in the data set provided and show that your code can detect it (TDD testing)

### Objective of The Analysis
Anomalies detection and machine failure prediction.

###Visualiz 
![newplot](https://user-images.githubusercontent.com/51690129/223624709-b9d03062-65bb-426a-a074-35bf543e47e9.png)

![newplot (1)](https://user-images.githubusercontent.com/51690129/223624730-b39ff1f0-73f7-4880-9efa-2b07d84f2a10.png)
![newplot (2)](https://user-images.githubusercontent.com/51690129/223624820-3a15df86-1aab-462f-882f-8afe2a25bddf.png)


### Methods used
1. Isolation Forest
![Screenshot from 2023-03-08 10-24-57](https://user-images.githubusercontent.com/51690129/223624017-90ca1f1e-6e01-4c82-ab6a-93cf6e79769e.png)

2. Kmeans Cluster
![Screenshot from 2023-03-08 10-25-21](https://user-images.githubusercontent.com/51690129/223624056-81efca33-d6b8-4fcb-a9b2-e06bdfd06c70.png)
![Screenshot from 2023-03-08 10-25-39](https://user-images.githubusercontent.com/51690129/223624082-42e572cc-81cc-4b98-8d49-5dc6573213a1.png)
![Screenshot from 2023-03-08 10-26-25](https://user-images.githubusercontent.com/51690129/223624195-9d426cbf-cc86-4bf7-be53-48848b2581da.png)

![Phases_p2p3_cluster](https://user-images.githubusercontent.com/51690129/223624231-90dce8e2-ae0f-413d-93d3-24fc60c60a0b.png)
![Phases_p1p3_cluster](https://user-images.githubusercontent.com/51690129/223624240-7759911d-57be-40e9-a4c2-39bd0f459466.png)
![Phases_p1p2_cluster](https://user-images.githubusercontent.com/51690129/223624243-62f7711d-a923-43ec-b98f-cb324bdc79ae.png)


3. PCA

![Motor current signature analysis](https://user-images.githubusercontent.com/51690129/223624327-15170a35-fe31-4601-80fe-1d938694cca4.png)
![Model-based vibration analysis](https://user-images.githubusercontent.com/51690129/223624341-a75ea87b-59d6-481d-8154-8222483f07fb.png)

4. VI analysis
![FFT](https://user-images.githubusercontent.com/51690129/223624403-31937f22-d31f-4ef6-adca-3c7d093a10a3.png)


### MLops
#### mlflow-fastapi 

1. Setup the working environment:
- Clone the repository in step 1 to local machine.
- Create new environment with Conda and activate it.
- Install required packages (the reference code base doesn't contain the "requirements.txt" so that I have to install manually).

2. Set up the MLFlow (install mlflow package and integrate with the source code) with the reference from [MLFlow documentation](https://www.mlflow.org/docs/latest/model-registry.html) and [this article](https://towardsdatascience.com/end-to-end-automl-train-and-serve-with-h2o-mlflow-fastapi-and-streamlit-5d36eedfe606).
- Start MLFlow with `mlflow ui`
- Customize code for MLFLow integration: log params and perform model registry.

**To Run the MLflow UI"
mlflow server \
       --backend-store-uri sqlite:///mlflow.db \
       --default-artifact-root ./artifacts \
       --host 0.0.0.0 \
       --port 5000
   ```
   
   ```python
   mlflow.set_tracking_uri("http://localhost:5000")
   ```
   
5. To fetch MLflow Model from the Model Registry (base on [this documentation](https://mlflow.org/docs/latest/model-registry.html#fetching-an-mlflow-model-from-the-model-registry)) 

6. Setup the FastAPI with the model loaded from MLFlow Registry
* Determine the input feature's schema (in `app/models.py`)
* Identify the model name and model version you want to load (in `main.py`).
* Run: `uvicorn app.main:app --reload`

**Note**: I haven't setup the FastApi code for this



