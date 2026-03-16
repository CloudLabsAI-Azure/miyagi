# Lab 1 : Containerizing Recommendation Service to Azure Container Apps

## Lab scenario 

In this lab, you'll explore the process of containerizing a recommendation service and deploying it to Azure Container Apps. Containerization has become a key strategy in modern application development and deployment, providing a consistent and reproducible environment across various stages of the software development lifecycle. Azure Container Apps, part of Microsoft's Azure cloud platform, offers a managed container service that enables developers to deploy and scale containerized applications seamlessly. 

## Lab objectives 

In this lab, you will complete the following tasks:

- Task 1: Set up configuration for Miyagi app
- Task 2: Run Miyagi frontend locally
- Task 3: Persist embeddings in Azure AI Search
- Task 4: Build Docker Images for the Recommendation Service
- Task 5: Push the Docker Image of the Recommendation service to the Container registry
- Task 6: Create a Container app for recommendation-service
- Task 7: Verify Recommendation Service using Swagger
- Task 8: Provision API Management Service 

### Duration: 50 minutes

## Task 1: Set up configuration for Miyagi app

In this task, you will set up the configuration for the Miyagi app by installing dependencies, configuring environment variables, and preparing the database for local development.

1. Open **Visual Studio Code** from the Lab VM desktop by double-clicking on it.

   ![](./Media/img-05.png)

   >**Note**: If **Join us in making promt-flow extension better!** window appears, click **No,thanks**.

   ![](./Media/image-rg-01.png)
   
1. In **Visual Studio Code** from the menu bar select **File (1) > Open Folder (2)**.

   ![](./Media/image-rg-02.png)

1. Within **File Explorer**, navigate to **C:\LabFiles\miyagi**, select **miyagi** (1), and click **Select Folder (2)**.

   ![](./Media/image-rg(003).png)

1. In **Visual Studio Code**, click on **Yes, I trust the authors** when the **Do you trust the authors of the files in this folder?** window is prompted.

   ![](./Media/image-rg-18.png) 
   
1. Expand **miyagi > ui** directory and verify that the **.env** file is present. 

1. Expand **miyagi/services/recommendation-service/dotnet** directory and verify that **appsettings.json** file is present.
  
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
   
   > **Note**: FYI, the above values/Keys/Endpoints/ConnectionString of Azure Resources are directly injected into the lab guide. Leave default settings for "cosmosDbContainerName": "recommendations" and "logLevel": "Trace".

      ![](./Media/appsetting-update.png)
   
1. After updating the values, save the file by pressing **CTRL + S**.

1. Navigate to **miyagi/sandbox/usecases/rag/dotnet** and verify **.env** file is present.
  
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

1. Open a new terminal by navigating to **miyagi/services/recommendation-service/dotnet** and right-click and, in the cascading menu, select **Open in Integrated Terminal**.

    ![](./Media/task4-1.png)

1. Run the following commands to start the recommendation service locally.

    ```
    dotnet build
    dotnet run
    ```

   > **Note**: Let the command run; meanwhile, you can proceed with the next step.

1. Open another tab in Edge, in the browser window, paste the following link

   ```
   http://localhost:5224/swagger/index.html 
   ```

   > **Note**: Refresh the page continuously until you get the Swagger page for the recommendation service as depicted in the image below.

   ![](./Media/miyagi2.png)


## Task 2: Run Miyagi frontend locally

In this task, you will run the Miyagi frontend locally by starting the development server and verifying the user interface for functionality and interaction.

1. Open a new terminal by navigating to **miyagi/ui** and right-click on **ui/typescript**, and in the cascading menu select **Open in Integrated Terminal**.

   ![](./Media/image-rg-25.png)

1. Run the following command to install the dependencies
   
    ```
    npm install --global yarn
    yarn install
    yarn dev
    ```

   > **Note**: Let the command run; meanwhile, you can proceed with the next step.

1. Open another tab in Edge, and browse the following URL:

   ```
   http://localhost:4001
   ```

   > **Note**: Refresh the page continuously until you get the **Miyagi app** running locally as depicted in the image below.
                       
   ![](./Media/b1.png)
   
   > **Note:** If you encounter any pop-up error, close it and proceed to the next task.

## Task 3: Persist embeddings in Azure AI Search

In this task, you will persist embeddings in Azure AI Search by configuring the service and using APIs to store and retrieve data efficiently.

1. Navigate back to the **swagger UI** page, scroll to the **Memory** section, click on **POST /datasets** for expansion, and click on **Try it out**.

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
      
1. In the **swagger UI** page, scroll down to the **Responses** section, review that it has been executed successfully by verifying that the status code is **200**.

    ![](./Media/swaggerUI-Responses.png)

1. Navigate back to the **Azure portal** tab, search and select **AI Search**.

    ![](./Media/ai-search1.png)    

1. In **Microsoft Foundry | AI Search** tab, select **acs-<inject key="DeploymentID" enableCopy="false"/>**.

1. In **acs-<inject key="DeploymentID" enableCopy="false"/>** Search service tab, click on **Indexes** **(1)** under **Search management**, and review the **miyagi-embeddings** **(2)** has been created.   

    ![](./Media/img-10-03.png)

    > **Note**: PClick the refresh button until the **Document Count** appears.

1. Once you have viewed the indexes in AI Search, navigate back to VS Code and  press **Ctrl + C** to stop the **Swagger UI** in the Node terminal.

1. From the **Terminal** select **dotnet** terminal, press **Ctrl + C** to stop the **recommendation service** ui page.

## Task 4: Build Docker Images for the Recommendation Service

In this task, you will build Docker images for the Recommendation service by creating a Dockerfile and using it to package the application for consistent deployment.

1. On the **Windows VM**, select **Start**, then double-click the **Docker Desktop** application to open it.


   ![](./Media/img-08.png)

    > **Note**: If Docker Desktop is already opened, then proceed with step 4.
   
1. In the **Docker Subscription Service Agreement** window, click **Accept**.

   ![](./Media/docker2.png)

1. In the **Welcome to Docker** window, click on **Skip**.

   ![](./Media/img-09.png)

   >**Note:** If you still encounter the **WSL update failed** error, click **Quit**, then open **PowerShell** as an administrator and run the following command:
   >
   > ```powershell
   > wsl --update
   > ```
   > On the **Docker Desktop** page, select **Try again** until the Docker engine starts.

1. In VS Code, navigate to **miyagi/services/recommendation-service/dotnet**, right-click on dotnet in the cascading menu, and select **Open in Integrated Terminal**.

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

1. Navigate back to **Docker Desktop**, from the left pane select **Images**.

   ![](./Media/img-10.png)

1. In the **Images** blade, notice **miyagi-recommendation (1)** image is created, select **Run (2)** icon.

   ![](./Media/img-11.png)

1. In the **Run a new container** window, select the dropdown arrow.

   ![](./Media/docker14-(1).png)

1. In the **Run a new container**, under **Ports** for **Host Port** enter **5224** and click on **Run**.

    ![](./Media/recommendation-port.png)

1. Click on **5224:80** URL link

   ![](./Media/recommendation-port-open.png)
   
1. You should be able to see the application running locally
   
   ![](./Media/docker-recommend.png)

## Task 5: Push the Docker Image of the Recommendation service to the Container registry

In this task, you'll push the **miyagi-recommendation** image to **ACR**.

1. Navigate back to the **Visual Studio Code** window and navigate to **miyagi/services/recommendation-service/dotnet** right-click on dotnet in cascading menu, select **Open in Integrated Terminal**

1. Run the following command to log in to the **Azure portal**.

    ```
    az login -u <inject key="AzureAdUserEmail" enableCopy="true"/> -p <inject key="AzureAdUserPassword" enableCopy="true"/>
    ```

    > **Note:** If you encounter the error **“az is not recognized”**, please run the following command: **Install-Module -Name Az -Repository PSGallery -Force**.Then reopen Visual Studio Code and run the **Step 02** command again.

1. Run the following command to log in to an **Azure Container Registry (ACR)** using the Azure CLI.
   
   ```
   az acr login -n <inject key="AcrUsername" enableCopy="true"/> -u <inject key="AcrUsername" enableCopy="true"/> -p <inject key="AcrPassword" enableCopy="true"/>
   ```

   ![](./Media/task2-5.png)
    
1. Run the following command to add the tag.

   ```
   docker tag miyagi-recommendation:latest <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest
   ```

1. Run the following command to push the image to the container registry.

   ```
   docker push <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest
   ```

   ![](./Media/task2-6.png)

## Task 6: Create a Container app for recommendation-service 

In this task, you'll create a container app for the recommendation service.

1. Run the following command to log in to the **Azure portal**.

   ```
   az login
   ```

1. This will redirect to **Microsoft login page**, select **Work or school account**, enter the username **<inject key="AzureAdUserEmail"></inject>** and password **<inject key="AzureAdUserPassword"></inject>**.

1. On the **Sign in to all apps, websites, and services on this device?** pop-up select **No, this app only**.

1. Navigate back to **Visual Studio Code**, and in the terminal press **Enter** when prompted to select the subscription.

1. Run the following command to create a **Container App environment**.

   ```
   az containerapp env create --name env-miyagi-<inject key="DeploymentID" enableCopy="true"/> --resource-group miyagi-rg-<inject key="DeploymentID" enableCopy="true"/> --location <inject key="Region" enableCopy="true"/>
   ```

1. Run the following command to create **Container App**.

   ```
   az containerapp create --name ca-miyagi-rec-<inject key="DeploymentID" enableCopy="true"/> --resource-group miyagi-rg-<inject key="DeploymentID" enableCopy="true"/> --image <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest --environment env-miyagi-<inject key="DeploymentID" enableCopy="true"/> --registry-server <inject key="AcrLoginServer" enableCopy="true"/> --registry-username <inject key="AcrUsername" enableCopy="true"/> --registry-password <inject key="AcrPassword" enableCopy="true"/>
   ```

1. Run the following command to enable **Container App ingress**.
   
   ```
   az containerapp ingress enable -n ca-miyagi-rec-<inject key="DeploymentID" enableCopy="true"/> -g miyagi-rg-<inject key="DeploymentID" enableCopy="true"/> --type external --allow-insecure --target-port 8080
   ```

## Task 7: Verify Recommendation Service using Swagger

In this task, you will verify the Recommendation Service using Swagger by accessing the API documentation, testing endpoints, and ensuring the service functions as expected.

1. In the **Azure Portal** page, in the **Search resources, services, and docs (G+/)** box at the top of the portal, enter **Container Apps (1)**, and then select **Container Apps (2)** under services.

   ![](./Media/container-app-select.png)

1. In the **Container Apps** blade, select **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](./Media/img-12.png)

1. In the **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>** page, from the left navigation pane, select **Ingress** **(1)** under **Networking** and click on **Endpoints** **(2)** URL link.

   ![](./Media/img-15.png)

1. You can view the **Miyagi Recommendation Service** website running through the Container Apps.

   ![](./Media/online-output-recommendation.png)   

## Task 8: Provision API Management Service 

In this task, you will provision the API Management Service by creating an instance, configuring settings, and setting up policies for efficient API management and security.

1. Navigate to **Search resources, services, and docs** on the **Azure portal** home page, search for **API Management services**, and click on it, and then click **+ Create**.

1. Provide the values as follows and click on **Review + Create** and again **Create.**

   - **Subscription (1)**: default selected subscription
   - **Resource Group (2)**: **miyagi-rg-<inject key="DeploymentID" enableCopy="true"/>**
   - **Region (3)**: **<inject key="Region" enableCopy="true"/>**
   - **Resource Name (4)**: **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>**
   - **Organization Name (5)**: **contoso**
   - **Administrator Email (6)**: **<inject key="AzureAdUserEmail" enableCopy="true"/>**
   - **Pricing Tier (7)**: **Basic (99.95% SLA)**

      ![](./Media/api-management-prov.png)

   >**Note**: Please continue with the next step as the deployment will take around 20-30 minutes to complete. 

1. Now, click on **Next** from the lower right corner to move to the next page.

## Summary

In this lab, you have accomplished the following:

- Configured the Miyagi app and ensured its functionality.
- Ran the Miyagi frontend locally for testing user interactions.
- Persisted embeddings in Azure AI Search for efficient retrieval.
- Built and pushed Docker images for the Recommendation Service.
- Created a container app and verified it using Swagger.

### Now click on **Next** from the lower right corner to move to the next page.

![](./Media/img-10-02.png)
