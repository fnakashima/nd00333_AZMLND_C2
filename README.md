
# Operationalizing Machine Learning
This project is part of the Udacity Azure ML Nanodegree. In this project, we build an Auto ML, run it with bank merketing dataset and deploy the best model to consume it as an endpoint.
In addition, we use Python SDK to enable logging by using Application Insights and also build Swagger documentation for the endpoint which is useful for developers.
Finally, we build an Azure ML pipeline and publish it as an endpoint to automate the whole process.

## Architectural Diagram
Here is an architectual diagram of this project.
![Project Architectural Diagram](/images/AzureML_architecture.png)

There are 7 steps in the project.
#### Authentication
Setting authentication is very important for the continuous flow of operations which can automate the flows by removing human interaction.
Azure Kubernetes service and Azure Container Instances are avalialbe for this purpose.
Using a service principal is a great way to allow authentication while reducing the scope of permissions, which enhances security.

#### Auto ML model
We use an Azure ML to train by using the bank merketing dataset and find the best model.

#### Deploy the best model
Once we find the best model, we can deploy the model as a HTTP endpoint so that it can be interacted from any external services.

#### Enable logging
Azure provides Application Insights for monitoring the service and you can also alanyse the performance of the service.
This can be enabled by the python SDK.

#### Consume model endpoints
Once the best model is deployed, we can now consume it via an HTTP API. The APIs exposed by Azure ML will use JSON to accept data and submit responses.
We also build a web based documentation of the API by using Swagger.

#### Create and publish a pipeline
Published pipelines allow external services to interact with them so that they can do work more efficiently.
We build an Azure ML pipleine, publish and run it in Jupyter Notebook.

#### Documentation
Finally we demonstrate all our work by using this README and a short screencast. 


## Key Steps
### Step 1: Authentication
In this project, this step was skipped as the lab provided by Udacity was used.

### Step 2: Automated ML Experiment
#### Create a bank marketing dataset
The [Bankmarketing dataset](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv) was used as a dataset for this project.
![Bank marketing dataset](/images/01_Step2_RegisteredDatasets.PNG)

#### Create an AutoML and run the experiment
An AutoML was created with the following configuration and was run. It took approximately 23 minutes.
* Task type: `Classification`
* Primary metric: `AUC weighted`
* Compute target: `Standard_DS12_v2` (4 cores, 28 GB RAM, 56 GB disk)
* Minimum number of nodes: `1`

![Experiment completed](/images/02_Step2_ExperimentCompletedDetails.PNG)

#### Find the best model
The best model was found and it was VotingEnsemble.
![Best model](/images/03_Step2_BestModelDetails.PNG)

### Step 3: Deploy the Best Model
The best model was deployed with the following configuration.
* Compute type: `Azure Container Instance`
* Authentication: `Enabled`
![Deploy best model](/images/03a_Step3_DeployBestModel.PNG)

It was displayed in the Endpoints after the deploy.
![Deployed best model](/images/03b_Step3_DeplyBestModel_Added.PNG)

### Step 4: Enable Application Insights
Application Insights was enabled by the following script.
![Enable Application Insights](/images/04a_Step4_EnableApplicationInsights.PNG)

After the run, it was enabled successfully.
![Application Insights enabled](/images/04_Step4_EnableApplicationInsights_Enabled.PNG)

Also logs were displayed by running the script as below.
![View logs](/images/05_Step4_RunningLogs.PNG)

### Step 5: Swagger Documentation
The swagger documentation for the endpoint of the best model was successfully built by the `swagger.sh` and `serve.py`.
![Swagger documentation](/images/06_Step5_SwaggerDocForBestModel.PNG)

### Step 6: Consume Model Endpoints
The response from the API was successfully received by running the `endpoint.py` as below.
![API response](/images/07_Step6_ConsumeEndpoint.PNG)

Additionally, the following performance results were retrieved by using Apache Benchmark.
![Apache Benchmark 1](/images/08_Step6_ApacheBenchmark1.PNG)
![Apache Benchmark 2](/images/09_Step6_ApacheBenchmark2.PNG)

### Step 7: Create, Publish and Consume a Pipeline
By running all the cells in `aml-pipelines-with-automated-machine-learning-step.ipynb`, the pipeline was successfully published.
![AzureML pipeline](/images/10_Step7_PipelineEndpoint.PNG)

Here is a details of the pipeline.
![Published pipeline](/images/12_Step7_PublishedPipelineOverview.PNG)
![Dataset with AutoML](/images/11_Step7_DatasetWithAutoML.PNG)

The pipeline endpoint was scheduled in Jupyter Notebook.
![Dataset with AutoML](/images/13_Step7_PipelineRunDetails.PNG)

It was shown in the Pipeleins in ML studio.
![Scheduled pipeline](/images/15_Step7_PipelineScheduledRun.PNG)


## Screen Recording
Here is a screencast for this project.

https://youtu.be/UO5gAQ2jZA0


## Future Improvements
* Use deep learning in AutoML run to have better scores (This requires additional time and cost)
* Increase experiment timeout duration for more training (This also requires additional time and cost)


## Standout Suggestions
* Apache Benchmark was used to analyse the performance of the endpoint.

