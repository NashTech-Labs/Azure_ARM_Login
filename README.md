# Azure_ARM_Login
This template uses an ARM service connection to connect to Azure resources with Service Principal Authentication (SPA). With an ARM service connection, you can use a pipeline to deploy to Azure resources without needing to reauthenticate each time.

## Parameters:

The pipeline requires the following parameters to be defined:


| Name  | Displayname | type | Default | Values | Opional/Required | Comments |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| serviceConnection | Azure Service Connection for acr registry or azure resource manager in your Azure pipeline | string | | | Required | This helps the module to authenticate with registry or azure cli |
| azureTaskType | Type of Azure Task | string | 'powershell' | 'powershell' / 'cli' | Optional | Required when **serviceConnectionType** is 'arm'| 
| imageACR | Azure Container Registry Name | string | | | Optional | Required when serviceConnectionType is 'arm' |
| stepname | Step Name | String | ARM | Optional | |It enables the step name to be defined | 

These parameters provide multiple use case options for the template, enable/disable flags for the utilization of different templates as per the requirements.


## Use Cases

You can directly call a particular template as per the requirement. for example: 

  ```yaml
  # azure-pipeline.yml
  resources:
  repositories:
    - repository: Template
      type: github
      name: your_username/Azure_ARM_Login
      ref: <respective branch name>
      endpoint: 'githubServiceConnectioNname'

  steps:
  # passing the parameters
  - template: ARM_Login_to_Azure_ACR.yaml@Template
    parameters:
      serviceConnection: ${{parameters.serviceConnection}}
      imageACR: ${{ parameters.imageACR }}
      stepname: 'BuildPush'
      azureTaskType: ${{parameters.azureTaskType}}
        
  
Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.

  ```
