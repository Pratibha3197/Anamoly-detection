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


### Methods used


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
   
   Run the `baseline_model.py` and check the MLFlow UI, you will see the new model in Models tab. 

5. Write the `load_model_with_mlflow.py` to fetch MLflow Model from the Model Registry (base on [this documentation](https://mlflow.org/docs/latest/model-registry.html#fetching-an-mlflow-model-from-the-model-registry)) 

6. Setup the FastAPI with the model loaded from MLFlow Registry

* Determine the input feature's schema (in `app/models.py`)
* Identify the model name and model version you want to load (in `main.py`).
* Run: `uvicorn app.main:app --reload`

**Note**: I haven't setup the FastApi code for this

### Dockerization



### Conclusion
