# Lab 1: Containerizing Recommendation service to Azure Container Apps

### Estimated Duration: 60 minutes

## Lab scenario
In this Lab, you'll explore the process of containerizing a recommendation service and deploying it to Azure Container Apps. Containerization has become a key strategy in modern application development and deployment, providing a consistent and reproducible environment across various stages of the software development lifecycle. Azure Container Apps, part of Microsoft's Azure cloud platform, offers a managed container service that enables developers to deploy and scale containerized applications seamlessly.  

## Lab objectives

In this lab, you will complete the following tasks:

- Task 1: Set up configuration for Miyagi app
- Task 2: Run Miyagi frontend locally
- Task 3: Persist embeddings in Azure AI Search
- Task 4: Build Docker Images for the Recommendation Service
- Task 5: Push the Docker Image of the Recommendation service to the Container registry
- Task 6: Create a Container app for recommendation-service
- Task 7: Verify Recommendation Service using Swagger

## Task 1: Set up configuration for Miyagi app

In this task, you will set up the configuration for the Miyagi app by installing dependencies, configuring environment variables, and preparing the database for local development.

1. Open **Visual Studio Code** from the Lab VM desktop by double-clicking on it.

   ![](./Media/vs.png)

   >**Note** If **Join us in making promt-flow extension better!** window prompted please click on **No,thanks**.

   ![](./Media/image-rg-01.png)
   
1. In **Visual Studio Code** from menu bar select **File(1)>open folder(2)**.

   ![](./Media/image-rg-02.png)

1. Within **File Explorer**, navigate to **C:\LabFiles\miyagi** select **miyagi (1)** click on **Select folder (2)**

   ![](./Media/image-rg(003).png)

1. In **Visual Studio Code**, click on **Yes, I trust the authors** when the **Do you trust the authors of the files in this folder?** window is prompted.

   ![](./Media/image-rg-18.png) 
   
1. Expand **miyagi>ui>typescript** directory and verify that **.env.** file is present.

   ![](./Media/L2T1S5.png)

1. Open **miyagi folder** and expand **services (1)/recommendation-service (2)/dotnet (3)** directory and verify that **appsettings.json (4)** file is present.

   ![](./Media/L2T1S6.png)

1. In the **appsettings.json** file, replace the following values for the variables below.

   | **Variables**                | **Values**                                                    |
   | ---------------------------- |---------------------------------------------------------------|
   | deploymentOrModelId          | **<inject key="CompletionModel" enableCopy="true"/>**         |
   | embeddingDeploymentOrModelId | **<inject key="EmbeddingModel" enableCopy="true"/>**          |
   | endpoint                     | **<inject key="OpenAIEndpoint" enableCopy="true"/>**          |
   | apiKey                       | **<inject key="OpenAIKey" enableCopy="true"/>**               |
   | azureCognitiveSearchEndpoint | **<inject key="SearchServiceuri" enableCopy="true"/>**        |
   | azureCognitiveSearchApiKey   | **<inject key="SearchAPIkey" enableCopy="true"/>**            |
   | cosmosDbUri                  | **<inject key="CosmosDBuri" enableCopy="true"/>**             |
   | blobServiceUri               | **<inject key="StorageAccounturi" enableCopy="true"/>**       |
   | bingApiKey                   | **<inject key="Bing_API_KEY" enableCopy="true"/>**           |
   | cosmosDbConnectionString     | **<inject key="CosmosDBconnectinString" enableCopy="true"/>** |
   
   > **Note**: FYI, the above values/Keys/Endpoints/ConnectionString of Azure Resources are directly injected into labguide. Leave default settings for "cosmosDbContainerName": "recommendations" and "logLevel": "Trace".

      ![](./Media/appsetting-update.png)
   
1. Once after updating the values, kindly save the file by pressing **CTRL + S**.

1. In the **miyagi** folder, expand **sandbox (1)/usecases (2)/rag (3)/dotnet (4)** and verify **.env (5)** file is present.

   ![](./Media/miyagi-image(111).png)
  
1. In the **.env** file, replace the following values for the variables below.

   | **Variables**                          | **Values**                                            |
   | ---------------------------------------| ------------------------------------------------------|
   | AZURE_OPENAI_ENDPOINT                  | **<inject key="OpenAIEndpoint" enableCopy="true"/>**  |
   | AZURE_OPENAI_CHAT_MODEL                | **<inject key="CompletionModel" enableCopy="true"/>** |
   | AZURE_OPENAI_EMBEDDING_MODEL           | **<inject key="EmbeddingModel" enableCopy="true"/>**  |
   | AZURE_OPENAI_API_KEY                   | **<inject key="OpenAIKey" enableCopy="true"/>**       |
   | AZURE_COGNITIVE_SEARCH_ENDPOINT        | **<inject key="SearchServiceuri" enableCopy="true"/>**|
   |AZURE_COGNITIVE_SEARCH_API_KEY          | **<inject key="SearchAPIkey" enableCopy="true"/>**    |
   
   ![](./Media/env1new.png)

1. Once after updating the values, kindly save the file by pressing **CTRL + S**.

1. Open a new terminal: by navigating **miyagi/services/recommendation-service/dotnet** and right-click on in cascading menu select **Open in Integrated Terminal**.

    ![](./Media/task4-1.png)

1. Run the following command to run the recommendation service locally
    ```
    dotnet build
    dotnet run
    ```

   **Note**: Let the command run; meanwhile, you can proceed with the next step.

1. Open another tab in Edge, in the browser window, paste the following link

   ```
   http://localhost:5224/swagger/index.html 
   ```

   **Note**: Refresh the page continuously until you get the Swagger page for the recommendation service as depicted in the image below.

   ![](./Media/miyagi2.png)


## Task 2: Run miyagi frontend locally

In this task, you will run the Miyagi app locally by starting the development server and verifying its functionality in your browser.

1. Open a new terminal: by navigating  **miyagi/ui** and right-click on **ui/typescript** , in cascading menu select **Open in Integrated Terminal**.

   ![](./Media/image-rg-25.png)

1. Run the following command to install the dependencies
   
    ```
    npm install --global yarn
    yarn install
    yarn dev
    ```

   **Note**: Let the command run; meanwhile, you can proceed with the next step.

1. Open another tab in Edge, and  browse the following

   ```
   http://localhost:4001
   ```

   **Note**: Refresh the page continuously until you get the Miyagi app running locally as depicted in the image below.
                       
   ![](./Media/b1.png)
   
## Task 3: Persist embeddings in Azure AI Search

In this task, you will learn how to persist embeddings in Azure AI Search by configuring the necessary settings and utilizing APIs for efficient data storage and retrieval.

1. Navigate back to the **swagger UI** page, scroll to **Memory** session, click on **POST /datasets** for expansion, and click on **Try it out**.

   ![](./Media/swaggerUI-memory.png)

1. Replace the code with the below code, and click on **Execute**.

     ```
     {
        "metadata": {
              "userId": "50",
              "riskLevel": "aggressive",
              "favoriteSubReddit": "finance",
              "favoriteAdvisor": "Jim Cramer"
            },
          "dataSetName": "intelligent-investor"
      }
      ```

      ![](./Media/swaggerUI-Execution.png)
      
1. In the **swagger UI** page, scroll down to the **Responses** section, review that it has been executed successfully by checking the code status is **200**.

    ![](./Media/swaggerUI-Responses.png)

1. Navigate back to the **Azure portal** tab, search and select **AI Search**.

    ![](./Media/ai-search1.png)    

1. In **Azure AI services | AI Search** tab, select **acs-<inject key="DeploymentID" enableCopy="false"/>**.

1. In **acs-<inject key="DeploymentID" enableCopy="false"/>** Search service tab, click on **Indexes** **(1)** under Search management, and review the **miyagi-embeddings** **(2)** has been created.   

   ![](./Media/L2T5S6.png)

   > **Note**: Please click on the refresh button till you view the **Document Count**.

1. Once you have viewed the indexes in AI Search, navigate back to VS Code and  press **Ctrl + C** to stop the **swagger UI** page for the node terminal.

1. From the **Terminal** select **dotnet** terminal, press **Ctrl + C** to stop the **recommendation service** ui page.

## Task 4: Build Docker Images for the Recommendation Service

In this task, you will build Docker images for the Recommendation service by creating a Dockerfile and using it to package the application for consistent deployment.

1. Open the **Docker** Application from the Lab VM desktop by double-clicking on it.

   ![](./Media/docker1.png)

    > **Note**: If Docker Desktop is already opened, then proceed with step 4.
   
1. In the **Docker Subscription Service Agreement** window, click **Accept**.

   ![](./Media/docker2.png)

1. In the **Welcome to Docker Desktop** window, click on **Continue without signing in**.

   ![](./Media/without-signin.png)

1. In the **Tell us about the work you do** window, click on **Skip**.

1. Navigate back to **Visual studio code** window and navigate to **miyagi folder** and expand **services (1)/recommendation-service (2)/dotnet (3)** right - click on dotnet in cascading menu, select **Open in integrated Terminal (4)**.

   ![](./Media/aks-04.png)

1. Run the following command to build a **Docker image**.

   ```
   docker build --no-cache -t miyagi-recommendation .   
   ```

   ![](./Media/task2-1.png)

   > **Note**: Please wait as this command may require some time to complete.

1. Run the following command to get the newly created image.

   ```
   docker images
   ```
   
   ![](./Media/task2-2.png)

1. Navigate back to **Docker desktop**, from the left pane select **Images**.

   ![](./Media/docker7.png)

1. In the **Images** blade, notice **miyagi-recommendation(1)** image is created, select **run(2)** icon .

   ![](./Media/docker13.png)

1. In the **Run a new container** window, select the dropdown arrow.

   ![](./Media/docker14-(1).png)

1. In the **Run a new container**, under **Ports** for **Host Port** enter **5224** and click on **Run**.

    ![](./Media/recommendation-port.png)

1. Click on **5224:80** URL link

   ![](./Media/recommendation-port-open.png)
   
1. You should be able to see the application running locally
   
   ![](./Media/docker-recommend.png)

## Task 5: Push the Docker Image of the Recommendation service to the Container registry

In this task, you'll push Miyagi-recommendation images to ACR. 

1. Navigate back to the **Visual studio code** window and navigate to **miyagi folder** and expand **services (1)/recommendation-service (2)/dotnet (3)** right - click on dotnet in cascading menu, select **Open in integrated Terminal (4)**.

    ![](./Media/aks-04.png)

1. Run the following command to log in to the **Azure portal**.

   ```
   az login
   ```

1. This will redirect to **Microsoft login page**, select your Azure account **<inject key="AzureAdUserEmail"></inject>**, and navigate back to the **Visual studio code**.

   ![](./Media/azurelogin.png)
    
1. Run the following command to log in to an **Azure Container Registry (ACR)** using the Azure CLI.
   
   ```
   az acr login -n <inject key="AcrUsername" enableCopy="true"/> 
   ```

   ![](./Media/task2-5.png)

   >**Note**: The command **az acr login -n <inject key="AcrLoginServer" enableCopy="false"/>** logs you into an Azure Container Registry (ACR) instance. It authenticates your session with the specified Azure Container Registry, allowing you to push and pull container images to and from the registry.   
    
1. Run the following command to add the tag.

   ```
   docker tag miyagi-recommendation:latest <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest
   ```

   >**Note**: The command **docker tag miyagi-recommendation:latest <inject key="AcrLoginServer" enableCopy="false"/>/miyagi-recommendation:latest** tags a local Docker image with a new name that includes the Azure Container Registry (ACR) name. By tagging the image this way, you prepare it to be pushed to the specified Azure Container Registry.

1. Run the following command to push the image to the container registry.

   ```
   docker push <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest
   ```

   ![](./Media/task2-6.png)
   
   >**Note**: The command **docker push <inject key="AcrLoginServer" enableCopy="false"/>/miyagi-recommendation:latest** uploads the specified Docker image, which has been tagged with the Azure Container Registry (ACR) name, to the ACR. This makes the image available in the ACR for deployment and use in various Azure services.   

## Task 6: Create a Container app for recommendation-service 

In this task, you'll be creating a container app for the recommendation.

1. Run the following command to create a **Container App environment**.

   > **Note**: Please replace **[DID]** with **<inject key="DeploymentID" enableCopy="true"/>** and **[Region]** with **<inject key="Region" enableCopy="true"/>**.

   ```
   az containerapp env create --name env-miyagi-[DID] --resource-group miyagi-rg-[DID] --location [Region]
   ```

1. Run the following command to create **Container App**.

   > **Note**: Please replace **[DID]** with **<inject key="DeploymentID" enableCopy="true"/>**, **[ACRname]** with **<inject key="AcrLoginServer" enableCopy="true"/>**, **[uname]** with **<inject key="AcrUsername" enableCopy="true"/>**, and **[password]** with **<inject key="AcrPassword" enableCopy="true"/>**.

   ```
   az containerapp create --name ca-miyagi-rec-[DID] --resource-group miyagi-rg-[DID] --image [ACRname]/miyagi-recommendation:latest --environment env-miyagi-[DID] --registry-server [ACRname] --registry-username [uname] --registry-password [password]
   ```

1. Run the following command to enable **Container App ingress**.

   > **Note**: Please replace **[DID]** with **<inject key="DeploymentID" enableCopy="true"/>**
   
   ```
   az containerapp ingress enable -n ca-miyagi-rec-[DID] -g miyagi-rg-[DID] --type external --allow-insecure --target-port 8080
   ```

## Task 7: Verify Recommendation Service using Swagger

In this task, you will verify the Recommendation Service using Swagger by accessing the API documentation, testing endpoints, and ensuring proper functionality of the service.

1. In the Azure Portal page, in the Search resources, services, and docs (G+/) box at the top of the portal, enter **Container Apps (1)**, and then select **Container Apps (2)** under services.

   ![](./Media/container-app-select.png)

1. In the **Container Apps** blade, select **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](./Media/container-ca-miyagi.png)

1. In the **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>** page, from left navigation pane select **Ingress** **(1)** under Networking session and click on **Endpoints** **(2)** URL link.

   ![](./Media/gg-4-1.png)

   > **Note**: If you don't see endpoints, open Azure Cloud Shell and run the following command.

   > **Note**: Please replace **[DID]** with **<inject key="DeploymentID" enableCopy="true"/>**.

   > ```sh
   > az containerapp ingress enable \
   >   --name ca-miyagi-rec-[DID] \
   >   --resource-group miyagi-rg-[DID] \
   >   --type external \
   >   --target-port 8080
   > ```

1. You can view the **Miyagi Recommendation service** website running through the Container Apps.

   ![](./Media/online-output-recommendation.png)    


## Summary

In this lab, you have accomplished the following:

- Configured the Miyagi app to ensure proper functionality and integration.
- Successfully ran the Miyagi frontend locally for testing and interaction.
- Persisted embeddings in Azure AI Search for efficient data retrieval.
- Built Docker images for the Recommendation service to facilitate deployment.
- Pushed the Docker image of the Recommendation service to the container registry for storage.
- Created a container app for the Recommendation service to enable cloud deployment.
- Verified the Recommendation service using Swagger to ensure correct API functionality.

### Now click on **Next** from the lower right corner to move to the next page.

![](./Media/n8.png)
