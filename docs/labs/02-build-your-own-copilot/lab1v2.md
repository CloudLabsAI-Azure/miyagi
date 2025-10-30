# Lab 2: Run Miyagi App Locally

### Estimated Duration: 60 minutes

In this lab, the focus is on configuring the Miyagi App for operational readiness. Subsequently, attention shifts to understanding the nuanced implementation of the Recommendation service. The practical phase involves executing the Recommendation service and deploying the Miyagi frontend locally for testing and development. A crucial step includes optimizing data retrieval efficiency by persisting embeddings in Azure AI Search. The project culminates with a broader exploration of the Miyagi App and Recommendation service, emphasizing a personalized user experience. This task-based approach ensures a systematic progression through the project intricacies, facilitating a comprehensive understanding and effective implementation.

## Lab objectives

You will be able to complete the following tasks:

- Task 1: Setup configuration for miyagi app
- Task 2: Understanding the implementation of the Recommendation service
- Task 3: Run recommendation service locally
- Task 4: Run miyagi frontend locally
- Task 5: Persist embeddings in Azure AI Search
- Task 6: Explore the Miyagi App and Recommendation service by Personalizing
  
### Task 1: Setup configuration for miyagi app

In this task, you will configure the Miyagi application by updating specific settings in Visual Studio Code. This involves replacing placeholder values in configuration files with the actual values for various Azure resources to ensure proper connectivity and functionality.

1. Open **Visual Studio Code** from the Lab VM desktop by double-clicking on it.

   ![](./Media/vs-01.png)

   >**Note**: If **Join us in making promt-flow extension better!** window prompted please click on **No,thanks**.

   ![](./Media/image-rg-01.png)
   
1. In **Visual Studio Code** from menu bar, select **File (1) > Open folder (2)**.

   ![](./Media/image-rg-02.png)

1. Within **File Explorer**, navigate to **C:\LabFiles\miyagi** select **miyagi (1)** click on **Select folder (2)**

   ![](./Media/image-rg(003).png)

1. In **Visual Studio Code**, click on **Yes, I trust the authors** when **Do you trust the authors of the files in this folder?** window prompted.

   ![](./Media/image-rg-18.png) 
   
1. Expand **miyagi>ui>typescript** directory and verify that **.env.** file is present. 

   ![](./Media/L2T1S5.png)

1. Open **miyagi folder** and expand **services (1)/recommendation-service (2)/dotnet (3)** directory and verify that **appsettings.json (4)** file is present.

   ![](./Media/L2T1S6.png)
  
1. Open the **appsettings.json** file and replace the following values for the variables below.

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
   
   > **Note**: FYI, the above values/Keys/Endpoints/ConnectionString of Azure Resources are directly injected to labguide. Leave default settings for "cosmosDbContainerName": "recommendations" and "logLevel": "Trace".

      ![](./Media/miyagi-image(17)1.png)
   
1. Once after updating the values kindly save the file by pressing **CTRL + S**.

1. In the **miyagi** folder, expand **sandbox (1)/usecases (2)/rag (3)/dotnet (4)** and verify **.env (5)** file is present.

   ![](./Media/miyagi-image(111).png)
  
1. In the **.env** file replace the following values for the variables below.

   | **Variables**                          | **Values**                                            |
   | ---------------------------------------| ------------------------------------------------------|
   | AZURE_OPENAI_ENDPOINT                  | **<inject key="OpenAIEndpoint" enableCopy="true"/>**  |
   | AZURE_OPENAI_CHAT_MODEL                | **<inject key="CompletionModel" enableCopy="true"/>** |
   | AZURE_OPENAI_EMBEDDING_MODEL           | **<inject key="EmbeddingModel" enableCopy="true"/>**  |
   | AZURE_OPENAI_API_KEY                   | **<inject key="OpenAIKey" enableCopy="true"/>**       |
   | AZURE_COGNITIVE_SEARCH_ENDPOINT        | **<inject key="SearchServiceuri" enableCopy="true"/>**|
   |AZURE_COGNITIVE_SEARCH_API_KEY          | **<inject key="SearchAPIkey" enableCopy="true"/>**    |
   
   ![](./Media/miyagi-image(18).png)
   
1. Once after updating the values kindly save the file by pressing **CTRL + S**.

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

<validation step="209e971c-dc3f-486b-b7c7-1096724301f7" />

### Task 2: Understanding the implementation of the Recommendation service

In this task, recommendation service implements RAG pattern using Semantic Kernel SDK. The details of the implementation are captured in the Jupyter Notebook in the folder miyagi/sandbox/usecases/rag/dotnet. You can open the notebook in VSCode and run the cells to understand step-by-step details of how the Recommendation Service is implemented. Pay special attention to how the RAG pattern is implemented using Semantic Kernel. Select kernel as .NET Interactive in the top right corner of the notebook.

1. In the Visual Studio Code, navigate to **miyagi folder (1)** and expand **sandbox (2)/usecases (3)/rag (4)/dotnet (5)** folder and select **Getting-started.ipynb (6)**.

   ![](./Media/miyagi-image19.png)

1. **Execute the notebook cell by cell** (using either Ctrl + Enter to stay on the same cell or Shift + Enter to advance to the next cell) and observe the results of each cell execution.
  

   > **Note**: Make sure **.Net Interactive** is in ready State, if not please wait for 2 to 3 minutes. If it is still not loading, kindly close and reopen Visual Studio. Also, please do not click on **Run All** option to execute all the cells at a time which may lead to exceed in token limit that results Error: 503 – Service unreachable. 

      ![](./Media/miyagi-image20.png)
   
   > **Note**: In case any issues or errors occur related to exceeding the call rate limit of your current OpenAI S0 pricing tier. , Please wait for 15 to 20 seconds and Re-run the cell

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

<validation step="560130f4-fca1-49e1-98a6-97ec61155364" />

### Task 3: Run recommendation service locally
In this task, you will run the recommendation service locally by using Visual Studio Code to build and run the service in the terminal and then verify its functionality by accessing the Swagger page in the browser.

1. To open a new terminal, naviagate to **miyagi (1)/services (2)/recommendation-service (3)/dotnet (4)** and right-click on **dotnet** in cascading menu select **Open in intergate Terminal (5)**.

    ![](./Media/task4-1.png)

1. Run the following command to run the recommendation service locally
    
   ```
   dotnet build
   dotnet run
   ```

   > **Note**: Let the command run, meanwhile you can proceed with the next step.
   > **Note**: The commands dotnet build and dotnet run are fundamental in .NET Core and .NET 5+ environments for building and running .NET applications locally on your machine.

1. Open another tab in Edge browser, in the browser window paste the following link

   ```
   http://localhost:5224/swagger/index.html 
   ```

   > **Note**: Refresh the page continuously until you get the swagger page for the recommendation service as depicted in the image below.

   ![](./Media/miyagi-image21.png)

### Task 4: Run miyagi frontend locally

In this task, you will run the miyagi frontend locally by installing dependencies using npm and yarn and then starting the development server. You will verify its functionality by accessing the local development server in the browser.

1. To open a new terminal, navigate to  **miyagi folder (1)**, then expand **ui (2)** and right-click on **ui/typescript (3)** folder , in cascading menu select **Open in integrated Terminal (4)**.

   ![](./Media/image-rg-25.png)

1. Run the following command to install the dependencies
   
    ```
    npm install --global yarn
    yarn install
    yarn dev
    ```

   > **Note**: Please wait till the command gets executed successfully. It will take up to 5 minutes. Once the **yarn dev** command starts executing wait for 2 minutes and proceed with the next step.
   
   > **Note**: These commands (npm install --global yarn, yarn install, and yarn dev) are indeed essential in JavaScript and TypeScript projects for managing dependencies and running scripts necessary to set up and run applications. They ensure that all required packages are installed (yarn install), and they execute development scripts (yarn dev) defined in the project's configuration (package.json).

1. Open a new tab in Edge browser, and browse the following URL:

   ```
   http://localhost:4001
   ```

   >**Note:** You can get the port from the logs in the terminal.

      ![](./Media/error-pop-up.png)

   >**Note:** If you encounter an **Unhandled Runtime Error** pop-up, close the pop-up and also dismiss the error message at the bottom left corner.

     ![](./Media/error-side.png)

   > **[!IMPORTANT]**<br>
   > Please do not close the VS Code as you will need the localhost running for the future tasks.

### Task 5: Persist embeddings in Azure AI Search

In this task, you will persist embeddings in Azure AI Search by executing a POST request in Swagger UI, verifying the execution, and then confirming the creation of the index in the Azure portal.

1. Navigate back to the **swagger UI** page, scroll to **Memory** session, click on **POST /dataset (1)** for expansion, and click on **Try it out (2)**.

   ![](./Media/miyagi-image22.png)

1. Replace the below **code (1)** with the below code, and click on **Execute (2)**.

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

     ![](./Media/miyagi-image(23).png) 
      
1. In the **swagger UI** page, Scroll down to the **Responses** session review that it has been executed successfully by checking the code status is **200**.

    ![](./Media/miyagi-image24.png)

1. Navigate back to the **Azure portal** tab, in Search resources, services and docs (G+/) box at the top of the portal, enter **AI Search (1)**, and then select **AI Search (2)** under services.

    ![](./Media/miyagi-image25.png)

1. In **AI Foundry | AI Search** tab, select **acs-<inject key="DeploymentID" enableCopy="false"/>**.

    ![](./Media/L2T5S5.png)
   
1. In **acs-<inject key="DeploymentID" enableCopy="false"/>** Search service tab, click on **Indexes** **(1)** under Search management, and review the **miyagi-embeddings** **(2)** has been created.   

   ![](./Media/L2T5S6.png)

   > **Note**: Please click on the refresh button still you can view the **Document Count**.

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

<validation step="32fe7dd9-0728-4b16-b975-374eb199044d" />

### Task 6: Explore the Miyagi App and Recommendation service  by Personalizing
In this task, you'll personalize the Miyagi App's Recommendation service by selecting a financial advisor and reviewing the recommendations. Then, you'll check the logs in Visual Studio Code and stop the services.

1. Navigate back to the **recommendation service** ui page, and click on **personalize** button.

    ![](./Media/miyagi-image28.png)

1. In the **Personalize** page, select your **Favorite Financial Advisor (1)** and choose **GPT-4 (2)** for the **Reasoning Engine** from the dropdown menu, then click on **Personalize (3)**.

   ![](./Media/miyagi-image126.png)

1. You should see the recommendations from the recommendation service in the Top Stocks widget.

   ![](./Media/miyagi-image30.png) 

1. Navigate to the **Visual Studio Code**, and click on **dotnet** from the terminal, you can go through the logs.

   ![](./Media/terminal-output.png)    

1. Once you view the logs, press **Ctrl + C** to stop the **swagger UI** page.

1. From the **Terminal** select **Node** terminal, press **Ctrl + C** to stop the **recommendation service** ui page.

   ![](./Media/miyagi-image31.png)

1. Now, click on **Next** from the lower right corner to move to the next page.

## Summary

In this Lab, you began with configuring the Miyagi App for operational readiness, followed by a detailed exploration of the Recommendation service's implementation. Practical execution involves running the Recommendation service and deploying the Miyagi frontend locally for testing. Enhancing data retrieval efficiency is a pivotal step, achieved by persisting embeddings in Azure AI Search. The project concludes with a broad exploration of the Miyagi App and Recommendation service, prioritizing a personalized user experience. This systematic approach ensures a thorough understanding and effective implementation throughout the project.

### You have successfully completed this lab. Now click on Next from the lower right corner to move to the next page.

![](./Media/next-page.png)