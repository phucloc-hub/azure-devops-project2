# Overview

Hello, I am Nghi, this is project 2 (CICD) in Nanodegree for DevOps Engineer using MS Azure from Udacity.

This project consists of flask application that is developed to predict housing prices in Boston (the model is already created by the instructor). 

This repositry demonstrate:
- Deploying the app in Azure CloudShell
- Deploying the app as a web server using Azure App Service.

If anything changed in it repository,  it will trigger the Github Action and also the Azure DevOps Pipelines to perform the CICD process and finally deploy to my app service.

## Badge

[![Python application test with Github Actions](https://github.com/Metan-CH4/azure-devops-project2.1/actions/workflows/pythonapp.yml/badge.svg)](https://github.com/Metan-CH4/azure-devops-project2.1/actions/workflows/pythonapp.yml)

## Project Plan

A [Trello](https://trello.com/b/3YsyayTe/build-cicd-pipeline-for-azure-devops) board to keep track of the tasks.

A [spreadsheet](project-schedule-h.xlsx) to manage the project plan.

## Instructions

Here is an architectural diagram:

![diagram](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/diagram.png?raw=true)

## Deploy the app in Azure Cloud Shell

In Azure Cloud Shell, clone the repo:
```
git clone git@github.com:Metan-CH4/azure-devops-project2.1.git
```
![screenshot-gitClone-AzureCloud](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/00%20-%20Clone.jpg?raw=true)


Change into the new directory:
```
cd azure-devops-project2.1
```

Change to branch "ci-to-git-action"

```
git checkout ci-to-git-action
```

Create a virtual environment:
```
python3 -m venv ~/.myrepo
```

Activate the virtual environment:
```
source ~/.myrepo/bin/activate
```

Install dependencies in the virtual environment and run tests:
```
make all
```
![make-all](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/02%20-%20Run%20make%20all%20from%20Local.png?raw=true)

Make change and test GitHub action
![screenshot-test-githubaction](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/03%20-%20Test%20GitHub%20Action.png?raw=true)

## Deploy the app to an Azure App Service

Create an App Service in Azure. 

Use this [file](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/commands.sh) to create new App Services

```
az webapp up -n azure-devops-project2
```

Next, create the pipeline in Azure DevOps. The basic steps are:

- Go to [https://dev.azure.com](https://dev.azure.com) and sign in.
- Create a new private project.
- Create a new service connection to ARM, select subscription and the app service.
- Create a new pipeline linked to your GitHub repo using GiThub YAML File.

Screenshot of the App Service:

![My WebApp](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/04%20-%20Azure%20Web%20App.png?raw=true)

Screenshot of Azure DevOps Project:

![My_DevOps](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/05%20-%20My%20DevOps%20.png?raw=true)

To test the app running in Azure App Service, edit line 28 of the make_predict_azure_app.sh script with the DNS name of your app. Then run the script:
```
./make_predict_azure_app.sh 
```

If it's working you should see the following output:

![screenshot-prediction](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/06%20-%20make%20prediction.jpg?raw=true)

You can also visit the URL of the App Service via the browser and you should see the following page:

![screenshot-browser](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/07%20-%20Test.png?raw=true)

View the app logs:

To view the log in Cloud Shell
```
az webapp log tail -g metal.ch4_rg_6319 -n azure-devops-project2
```
![screenshot-log-webapp](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/08%20-%20Log.png?raw=true)


> 

## Load test

I use locust to perform load test on my local computer. 

Install locust:
```
pip install locust
```

Start load test:
```
locust -f locustfile.py --host https://azure-devops-project2.azurewebsites.net/ --users 500 --spawn-rate 5 
```
Open a browser and go to [http://localhost:8089](http://localhost:8089) then click Start Swarming:

![screenshot-loadtest#1](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/09%20-%20Load%20test%20%231.png?raw=true)
![screenshot-loadtest#2](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/10%20-%20Load%20test%20%232.png?raw=true)
![screenshot-loadtest#3](https://github.com/Metan-CH4/azure-devops-project2.1/blob/main/evidences/11%20-%20Load%20test%20%233.png?raw=true)

## Future Enhancements
- Creating a UI for making predictions.
- Adding test cases.
- Deploying my app with AKS.

## Demo 
Demo Video on Youtube 
https://www.youtube.com/watch?v=yHDnCFm9pww&ab_channel=khuonghoang
