# Docker Image Build and Azure Web App Deployment Pipeline

This Azure DevOps pipeline automates the process of building a Docker image, pushing it to an Azure Container Registry, and deploying it to an Azure Web App. The pipeline is triggered when changes are pushed to the `main` branch of the repository.

## Pipeline Overview

### Pipeline Structure
- **Trigger**: The pipeline is triggered when changes are pushed to the `main` branch.

### Variables
- `dockerRegistryServiceConnection`: Azure Container Registry service connection established during pipeline creation.
- `imageRepository`: The name of the Docker image repository.
- `containerRegistry`: The Azure Container Registry where the Docker image will be pushed.
- `dockerfilePath`: The path to the Dockerfile.
- `tag`: The unique tag for the Docker image, typically the Build ID.
- `vmImageName`: The name of the agent VM image.

### Stages and Jobs
- **Stage: Build**
  - **Job: Build**
    - Uses an Ubuntu agent for building the Docker image.
    - Builds and pushes the Docker image to the specified container registry.
    - Deploys the image to an Azure Web App staging slot.

## Getting Started

1. Configure the variables in your Azure DevOps pipeline according to your specific project and Azure settings.

2. Ensure you have an Azure service connection in Azure DevOps to access Azure resources.

3. Set up the necessary environment, Dockerfile, and application code in your repository.

4. Push changes to the `main` branch to trigger the pipeline.






# Backend Docker Image Build and Infrastructure Deployment Pipeline

This Azure DevOps pipeline automates the process of building a Docker image, pushing it to an Azure Container Registry, and deploying it to Azure infrastructure. The pipeline is triggered when changes are pushed to the `main` branch of the repository.

## Pipeline Overview

### Pipeline Structure
- **Trigger**: The pipeline is triggered when changes are pushed to the `main` branch.

### Variables
- `tag`: The unique tag for the Docker image, typically the Build ID.
- `vmImageName`: The name of the agent VM.
- Other variables may be defined in group-specific variable groups.

### Stages and Jobs
- **Stage: Build**
  - **Job: BuildAndTest**
    - Builds the Docker image.
    - Runs unit tests and publishes test results.
    - Copies ARM templates and publishes code coverage reports.
    - Publishes Docker image to a container registry.

- **Stage: DeployToDev**
  - Deploys infrastructure to the Dev environment using ARM templates.

- **Stage: DeployToTest**
  - Deploys infrastructure to the Test environment using ARM templates.

- **Job: DeployInfrastructure**
  - Deploys infrastructure using downloaded ARM templates and parameters.

## Getting Started

1. Configure the variables and parameter values in your Azure DevOps pipeline according to your specific project and Azure settings.

2. Ensure you have an Azure service connection in Azure DevOps to access Azure resources.

3. Set up the necessary environment, Dockerfile, application code, and ARM templates in your repository.

4. Push changes to the `main` branch to trigger the pipeline.




# Server Deployment Pipeline

This Azure DevOps pipeline is designed to deploy code to a production environment. It consists of two stages: Build and DeployToProd.

## Pipeline Overview

### Pipeline Structure
- **Triggers**: The pipeline is triggered when changes are pushed to the `main` or `production` branches of the repository.

### Stages and Jobs

- **Stage: Build**
  - **Job: Build**
    - Copies necessary files to prepare for deployment.
    - Uploads artifacts to the pipeline for deployment.

- **Stage: DeployToProd**
  - **Job: VMDeploy**
    - Deploys code to a production environment, specifically a Virtual Machine.
    - Downloads artifacts from the build stage.
    - Executes scripts to set up prerequisites and deploy the application.

## Getting Started

1. Configure your triggers to match your branching strategy and determine when the pipeline should run.

2. Customize the deployment scripts in the `DeployToProd` stage to match your deployment requirements.

3. Ensure that the production environment (Virtual Machine) is set up with the necessary dependencies for your application.

4. Push changes to the `main` or `production` branch to trigger the pipeline.





## Pipeline Documentation

For more details on using this pipeline, refer to the official Azure DevOps documentation:
- [Azure DevOps Docker Pipeline](https://docs.microsoft.com/azure/devops/pipelines/languages/docker)

## Author

*Mohamed Mahrous*

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
