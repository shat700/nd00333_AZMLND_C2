
# Operationalizing Machine Learning for Bank Marketing Dataset

## Overview 
This project is part of the Udacity Azure ML Nanodegree. In this project, we perform AutoML on the dataset, deploy the best model obtained from AutoML as a RESTful webservice, consume endpoints to interact with the deployed model in Azure ML Studio and perform pipeline automation to improve machine learning operations.

## Architectural Diagram
![Architecture](Architecture.png)

## Key Steps

### 1. Authentication: 
This step plays a key role in maintaining a uninterrupted flow of operations. Human intervention slows down the process. Therefore, authentication with automation is considered as an ideal scenario. A 'Service Principal' is one of the best examples of authentication where the user role is defined with user specific permissions.

### 2. Automated ML Experiment for Best Model
In order to create an AutoML experiment, we first login into the AzureML portal and create a new compute for the new experiment. The virtual machine size chosen for the compute cluster is 'Standard_DS12_v2' with 1 as the minimum number of nodes. The experiment takes about 1 hour for completion with concurrency of 5. 

#### Registered Datasets

![Registereddatasets](Registereddatasets.png)

#### AutoML experiment completion

![Expcompleted](Expcompleted.png)

![Experimentcompleted1](Experimentcompleted1.png)

#### Best Model: VotingEnsemble

![Bestautomlmodel](Bestautomlmodel.png)

### 3. Deploy the best model
Deployment is the delivery of the best trained model into production so that it can be consumed by others. The best model obtained in the AutoML run is 'VotingEnsemble' with the highest accuracy of 0.91988. In order to deploy, we configure the deployment settings by enabling authentication and using Azure Container Instance (ACI) as it quickly deploys compute instances and is simple to use.

![Successfuldeployment](Successfuldeployment.png)

### 4. Enable logging
This is a crucial step to 'Enable Application Insights'. Application insights is a tool that helps in detecting anomalies and visualizing performance. It can be enabled before or after deployment and can be modified with the SDK. In this project, we enable application insights after deployment by adding a specific command to the python SDK. The modified python script displaying logs.

#### Application Insights Enabled

![Insightsenabled](Insightsenabled.png)

#### Python SDK run

![logsrun](logsrun.png)

### 5. Swagger Documentation
Swagger is a tool that helps build, document, and consume RESTful web services deployed in Azure ML Studio. It further explains what types of HTTP requests an API can consume, in this case like POST and GET. A swagger.json is provided in the endpoints section of Azure that is used to create a web site. This localhost website documents the HTTP endpoint for a deployed model. After running the swagger.sh and serve.py scripts, the webpage displays the contents of the API for the model along with different HTTP requests supported.

#### Swagger Website 

![swaggerweb](swaggerweb.png)

#### serve.sh script run on port 8000

![servescriptrun](servescriptrun.png)

#### API Contents

![APIcontents](APIcontents.png)

### 6. Consume Model Endpoints

In this project, the deployed service is consumed via an HTTP API. We initiate an input request, in this case via an HTTP POST request method to submit data. The HTTP GET is another request method to retrieve information from a web server. This creates a bi-directional flow of allowed information in Azure. 
In order to consume deployed service, we modify the URI and key to match the primary key for our service and RESTful URI generated after deployment. The execution of the endpoint.py script after modification gives output.

#### API for the Model

![ModelAPI](ModelAPI.png)

#### Pipeline runs

![Pipeline-runs](Pipeline-runs.png)

#### Pipeline endpoint

![Pipeline-endpoint](Pipeline-endpoint.png)

#### Run Details Widget

![RunDetailsWidget](RunDetailsWidget.png)

#### Published Pipeline Overview

![publishedpipelineoverview](publishedpipelineoverview.png)

#### Consume endpoint

![jsonoutput](jsonoutput.png)

## Future Improvements
Benchmarking can be done using Apache Benchmark command-line tool to keep the performance of the model in check and above a standard level. It is used to determine the 'response time' in seconds for the deployed model. Another suggestion would be to try different models to get the best possible one. This couldn't be done due to cost incurred by using the Azure account. 
The time taken for the experiment was approximately an hour. If we reduce the duration for the experiment or increase the number of processes running parallely i.e. concurrency, the experiment will be faster and time can be saved. Also, the use of Kubenetes service can be helpful in case we add more data to the existing dataset as it expands and contracts on demand. 

## Screen Recording
https://youtu.be/WXlqdmWif78

## Standout Suggestions Performed
AutoML experiment when run against column 'contact', the best model was found to be 'VotingEnsemble' and accuracy was calculated to be 0.94264 which is higher than in the case we considered in the project.
I chose the contact column since it is a crucial one in this dataset, therefore it provides a better performing model.

![BestModel](BestModel.png)
