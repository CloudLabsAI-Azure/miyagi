# Lab 1 - Run Miyagi App Locally

## Overview

In this lab, the focus is on configuring the Miyagi App for operational readiness. Subsequently, attention shifts to understanding the nuanced implementation of the Recommendation service. The practical phase involves executing the Recommendation service and deploying the Miyagi frontend locally for testing and development. A crucial step is optimizing data retrieval efficiency by persisting embeddings in Azure AI Search. The project culminates with a broader exploration of the Miyagi App and Recommendation service, emphasizing a personalized user experience. This task-based approach ensures a systematic progression through the project intricacies, facilitating a comprehensive understanding and effective implementation.

## Lab objectives
In this lab, you will complete the following tasks:

- Task 1: Set up configuration for Miyagi app
- Task 2: Understanding the implementation of the Recommendation service
- Task 3: Run the recommendation service locally
- Task 4: Run the Miyagi frontend locally
- Task 5: Persist embeddings in Azure AI Search
- Task 6: Explore the Miyagi App and Recommendation service  by Personalizing

## Task 1: Set up configuration for the Miyagi app

In this lab, you will configure the Miyagi app by setting up the environment, installing dependencies, and preparing the database for a seamless development experience.

1. Open **Visual Studio Code** from the Lab VM desktop by double-clicking on it.

   ![](./Media/img-05.png)

   >**Note** If the **Join us in making promt-flow extension better!** window is prompted, click on **No,thanks**.

   ![](./Media/image-rg-01.png)
   
1. In **Visual Studio Code** from menu bar select **File(1)** > **open folder(2)**.

   ![](./Media/image-rg-02.png)

1. Within **File Explorer**, navigate to **C:\LabFiles\miyagi** select **miyagi** (1) and click **Select folder (2)**

   ![](./Media/image-rg(003).png)

1. In **Visual Studio Code**, click on **Yes, I trust the authors** when the **Do you trust the authors of the files in this folder?** window is prompted.

   ![](./Media/image-rg-18.png) 
   
1. Expand **miyagi > ui** directory and verify that **.env** file is present. 

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
   
   > **Note**: FYI, the above values/Keys/Endpoints/ConnectionString of Azure Resources are directly injected into labguide. Leave default settings for "cosmosDbContainerName": "recommendations" and "logLevel": "Trace".

      ![](./Media/appsetting-update.png)
   
1. Once the values are updated, save the file by pressing **CTRL + S**.

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

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

<validation step="eb73d21f-c370-4eba-9380-8d78b6bfc326" />

## Task 2: Understanding the implementation of the Recommendation service

In this lab, you will explore the implementation of the Recommendation service, focusing on its algorithms and data processing methods to deliver personalized suggestions.

Recommendation service implements RAG pattern using Semantic Kernel SDK. The details of the implementation are captured in the Jupyter notebook in the folder miyagi/sandbox/usecases/rag/dotnet. You can open the notebook in VSCode and run the cells to understand step-by-step details of how the Recommendation Service is implemented. Pay special attention to how the RAG pattern is implemented using Semantic Kernel. Select the kernel as **.NET Interactive** in the top right corner of the notebook.

1. In the Visual Studio Code, navigate to **miyagi/sandbox/usecases/rag/dotnet** folder and select **Getting-started.ipynb**

   ![](./Media/image-rg-23.png)

1. **Execute the notebook cell by cell** (using either Ctrl + Enter to stay on the same cell or Shift + Enter to advance to the next cell) and observe the results of each cell execution.
  
   > **Note**: Make sure **.Net Interactive** is in ready State, if not please wait for 15 to 20 seconds. Also, please do not click on the **Run All** option to execute all the cells at a time,e this may lead to exceeding the token limit, resulting in the error: 503 – Service unreachable. 

      ![](./Media/run.png)

   > **Note**: Ensure that the **Python extension** is installed before running the cells.
   
   > **Note**: Ensure to click on **Work or School Account** when a window opens and provide the username and password
   
   > **Note**: In case any issues or errors occur related to the exceeded call rate limit of your current OpenAI S0 pricing tier. Please wait for 15 to 20 seconds and re-run the cell

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:

  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

<validation step="571b621e-6e53-4fbc-b3ec-6e614bc779a7" />

## Task 3: Run recommendation service locally

In this lab, you will set up the environment, install necessary dependencies, and run the Recommendation service locally to test and develop features effectively.

1. Open a new terminal: by navigating **miyagi/services/recommendation-service/dotnet** and right-click on in cascading menu select **Open in Integrated Terminal**.

    ![](./Media/task4-1.png)

1. Run the following commands to start the recommendation service locally:

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


## Task 4: Run miyagi frontend locally

1. Navigate back to the VS code, Open a new terminal by navigating to **miyagi/ui** and right-click on **ui/typescript** , in cascading menu select **Open in Integrated Terminal**.

   ![](./Media/image-rg-25.png)

1. Run the following command to install the dependencies
   
    ```
    npm install --global yarn
    yarn install
    yarn dev
    ```

   > **Note**: Let the command run; meanwhile, you can proceed with the next step.

1. Open another tab in Edge, and  browse the following

   ```
   http://localhost:4001
   ```

   > **Note**: Refresh the page continuously until you get Miyagi app running locally as depicted in the image below.
                       
   ![](./Media/b1.png)

   > **Note**: If you encounter any pop-up error, close it and proceed to the next task.
   
## Task 5: Persist embeddings in Azure AI Search

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
      
1. In the **swagger UI** page, scroll down to the **Responses** section, review that it has been executed successfully by verifying that the status code is **200**.

    ![](./Media/swaggerUI-Responses.png)

1. Navigate back to the **Azure portal** tab, search and select **AI Search**.

    ![](./Media/ai-search1.png)    

1. In **Microsoft Foundry | AI Search** tab, select **acs-<inject key="DeploymentID" enableCopy="false"/>**.

1. In **acs-<inject key="DeploymentID" enableCopy="false"/>**, from the left navigation menu click on **Indexes** **(1)** under **Search management**, and review the **miyagi-embeddings** **(2)** has been created.   

    ![](./Media/search-service.png)

    > **Note**: Click the refresh button to view the **Document Count**.

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
  > - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
  > - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
  > - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

<validation step="07efcc74-3b48-4da3-8be6-00bf71986f9e" />

## Task 6: Explore the Miyagi App and Recommendation service  by Personalizing

1. Navigate back to the **recommendation service** UI page, and click on **Personalize** button.

    ![](./Media/service-personalize.png)

1. In the **personalize** page, select your **financial advisor** from the drop-down, and click on **Personalize**.

   ![](./Media/financial-advisor.png)  

1. You should see the recommendations from the recommendation service in the Top Stocks widget.

   ![](./Media/financial-advisor-output.png) 

1. Navigate to the **Visual Studio Code**, and click on **dotnet** from the terminal, and you can go through the logs.

   ![](./Media/recommend-log.png)    

1. Once you view the logs, press **Ctrl + C** to stop the **swagger UI** page.

1.  From the **Terminal** select **node** terminal, press **Ctrl + C** to stop the **recommendation service** ui page.

## Summary

In this lab, you have accomplished the following:

- Installed dependencies and configured the database for the Miyagi app.
- Explored algorithms and methods used in the Recommendation service.
- Launched the Recommendation service locally and verified its functionality.
- Executed the Miyagi frontend locally to test user interactions.
- Configured and stored embeddings in Azure AI Search successfully.
- Personalized recommendations in the Miyagi app and tested user preference responses.

### You have successfully completed the lab
