# Lab 1 - Run Miyagi App Locally

In this lab, the focus is on configuring the Miyagi App for operational readiness. Subsequently, attention shifts to understanding the nuanced implementation of the recommendation service. The practical phase involves executing the recommendation service and deploying the Miyagi frontend locally for testing and development. A crucial step includes optimizing data retrieval efficiency by persisting embeddings in Azure AI Search. The project culminates with a broader exploration of the Miyagi app and recommendation service, emphasizing a personalized user experience. This task-based approach ensures a systematic progression through the project intricacies, facilitating a comprehensive understanding and effective implementation.

### Task 1: Setup configuration for the Miyagi app

1. Open **Visual Studio Code** from the Lab VM desktop by double-clicking on it.

   ![](./Media/vs.png)

   >**Note:** If the **Join us in making promt-flow extension better!** window is prompted, please click on **No, thanks**.

   ![](./Media/image-rg-01.png)
   
1. In **Visual Studio Code**, from the menu bar, select **File(1)>open folder(2)**.

   ![](./Media/image-rg-02.png)

1. Within **File Explorer**, navigate to **C:\LabFiles\miyagi**. Select **miyagi(1)** and click on **Select folder(2)**.

   ![](./Media/image-rg(003).png)

1. In **Visual Studio Code**, click on **Yes, I trust the authors** when **Do you trust the authors of the files in this folder?** window prompted.

   ![](./Media/image-rg-18.png) 
   
1. Expand the **miyagi>ui** directory and verify that the **.env.** file is present. 

1. Expand the **miyagi/services/recommendation-service/dotnet** directory and verify that the **appsettings.json** file is present.
  
1. In the **appsettings.json** file, replace the following values for the variables below:

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
   
   > **Note**: FYI, the above values/Keys/Endpoints/ConnectionString for Azure Resources are directly injected into the lab guide. Leave default settings for "cosmosDbContainerName": "recommendations" and "logLevel": "Trace."

      ![](./Media/appsetting-update.png)
   
1. Once you have updated the values, kindly save the file by pressing **CTRL + S**.

1. Navigate to **miyagi/sandbox/usecases/rag/dotnet** and verify the **.env** file is present.
  
1. In the **.env** file, replace the following values for the variables below:

   | **Variables**                          | **Values**                                            |
   | ---------------------------------------| ------------------------------------------------------|
   | AZURE_OPENAI_ENDPOINT                  | **<inject key="OpenAIEndpoint" enableCopy="true"/>**  |
   | AZURE_OPENAI_CHAT_MODEL                | **<inject key="CompletionModel" enableCopy="true"/>** |
   | AZURE_OPENAI_EMBEDDING_MODEL           | **<inject key="EmbeddingModel" enableCopy="true"/>**  |
   | AZURE_OPENAI_API_KEY                   | **<inject key="OpenAIKey" enableCopy="true"/>**       |
   | AZURE_COGNITIVE_SEARCH_ENDPOINT        | **<inject key="SearchServiceuri" enableCopy="true"/>**|
   |AZURE_COGNITIVE_SEARCH_API_KEY          | **<inject key="SearchAPIkey" enableCopy="true"/>**    |
   
   ![](./Media/env1new.png)

1. Once you have updated the values, kindly save the file by pressing **CTRL + S**.

### Task 2: Understanding the implementation of the recommendation service

The recommendation service implements RAG patterns using the Semantic Kernel SDK. The details of the implementation are captured in the Jupyter notebook in the folder miyagi/sandbox/usecases/rag/dotnet. You can open the notebook in VSCode and run the cells to understand the step-by-step details of how the recommendation service is implemented. Pay special attention to how the RAG pattern is implemented using the Semantic Kernel. Select kernel as .NET Interactive in the top right corner of the notebook.

1. In Visual Studio Code, navigate to the **miyagi/sandbox/usecases/rag/dotnet** folder and select **Getting-started.ipynb**.

   ![](./Media/image-rg-23.png)

1. **Execute the notebook cell by cell** (using either Ctrl + Enter to stay on the same cell or Shift + Enter to advance to the next cell) and observe the results of each cell execution.
  
   > **Note**: Make sure the **.Net Interactive** is in a ready state. If not, please wait for 15 to 20 seconds. Also, please do not click on the **Run All** option to execute all the cells at a time, which may lead to exceeding the token limit that results in Error: 503 – Service unreachable. 

      ![](./Media/run.png)

   > **Note**: In case any issues or errors occur related to exceeding the call rate limit of your current OpenAI S0 pricing tier, please wait for 15 to 20 seconds and re-run the cell.

### Task 3: Run the recommendation service locally

1. Open a new terminal by navigating to **miyagi/services/recommendation-service/dotnet** and right-clicking on the cascading menu and selecting **Open in intergate Terminal**.

    ![](./Media/task4-1.png)

1. Run the following command to run the recommendation service locally:
    ```
    dotnet build
    dotnet run
    ```

   **Note**: Let the command run; in the meantime,  you can proceed with the next step.

1. Open another tab in Edge, and in the browser window, paste the following link:

   ```
   http://localhost:5224/swagger/index.html 
   ```

   **Note**: Refresh the page continuously until you get the swagger page for the recommendation service as depicted in the image below.

   ![](./Media/miyagi2.png)


### Task 4: Run the Miyagi frontend locally

1. Open a new terminal by navigating to **miyagi/ui** and right-clicking on **ui/typescript**. In the cascading menu, select **Open in intergate Terminal**.

   ![](./Media/image-rg-25.png)

1. Run the following command to install the dependencies:
   
    ```
    npm install --global yarn
    yarn install
    yarn dev
    ```

   **Note**: Let the command run; in the meantime, you can proceed with the next step..

1. Open another tab in Edge and browse the following:

   ```
   http://localhost:4001
   ```

   **Note**: Refresh the page continuously until you get the Miyagi app running locally, as depicted in the image below.
                       
   ![](./Media/miyagi1.png)
   
### Task 5: Persist embeddings in Azure AI Search

1. Navigate back to the **swagger UI** page, scroll to **Memory** session, click on **POST/dataset** for expansion, and click on **Try it out**.

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
      
1. In the **swagger UI** page, scroll down to the **Responses** session review and confirm that it has been executed successfully by checking that the status code is **200**.

    ![](./Media/swaggerUI-Responses.png)

1. Navigate back to the **Azure portal** tab, search, and select **AI Search**.

    ![](./Media/ai-search1.png)    

1. In the **Azure AI services | AI Search** tab, select **acs-<inject key="DeploymentID" enableCopy="false"/>**.

1. In the **acs-<inject key="DeploymentID" enableCopy="false"/>** Search service tab, click on **Indexes** **(1)** under Search Management, and review the **miyagi-embeddings** **(2)** that have been created.

    ![](./Media/search-service.png)

    > **Note**: Please click on the refresh button while you view the **Document Count**.

### Task 6: Explore the Miyagi app and recommendation service by personalizing

1. Navigate back to the **recommendation service** I page and click on the **personalize** button.

    ![](./Media/service-personalize.png)

1. On the **personalize** page, select your **financial advisor** from the drop-down menu and click on **Personalize**.

   ![](./Media/financial-advisor.png)  

1. You should see the recommendations from the recommendation service in the Top Stocks widget.

   ![](./Media/financial-advisor-output.png) 

1. Navigate to **Visual Studio Code** and click on **dotnet** from the terminal. From there, you can go through the logs.

   ![](./Media/recommend-log.png)    

1. Once you view the logs, press **Ctrl + C** to stop the **swagger UI** page.

1.  From the **Terminal**, select **Node** terminal and press **Ctrl + C** to stop the **recommendation service** UI page.

1. Now, click on **Next** from the lower right corner to move to the next page.

## Summary

In this lab, you began with configuring the Miyagi app for operational readiness, followed by a detailed exploration of the recommendation service's implementation. Practical execution involves running the recommendation service and deploying the Miyagi frontend locally for testing. Enhancing data retrieval efficiency is a pivotal step, achieved by persisting embeddings in Azure AI Search. The project concludes with a broad exploration of the Miyagi app and recommendation service, prioritizing a personalized user experience. This systematic approach ensures a thorough understanding and effective implementation throughout the project.
