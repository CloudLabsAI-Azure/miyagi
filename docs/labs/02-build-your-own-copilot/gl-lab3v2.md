# Lab 3: Expose OpenAI through API Management Service

## Lab scenario

In this lab, you'll be verifying and creating APIs in the deployed **API Management Service** to update the Docker image for the Recommendation service. The revision of the Recommendation Service from the Container App reflects a meticulous approach to maintaining and optimizing containerized applications within the project's scope.

## Lab objectives 
In this lab, you will complete the following tasks:

- Task 1: Verify the API Management Service and create an API with Operations
- Task 2: Update the Recommendation Service configuration to access Azure OpenAI through APIM
- Task 3: Verify that the Recommendation Service accesses Azure OpenAI through APIM

## Task 1: Verify the API Management Service and create an API with Operations

In this task, you will verify the API Management Service and create an API with operations by defining endpoints, setting policies, and testing the functionality to ensure proper integration and management of your APIs.

1. Navigate to the **Azure portal**, open the resource group named **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, and select the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service from the resources list.

   ![](./Media/lab3-t1-s1.png)

1. In the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service, click **APIs** **(1)** under **APIs** section from the left menu and select **HTTP** **(2)** under Define a new API to create an HTTP API.

   ![](./Media/lab3-t1-s2.png)

1. Enter the following values in the Create an HTTP API pane:
   
   | **Parameter**        | **Values**           | 
   | -------------------- | -------------------- | 
   | API Type **(1)**     | **Full**            | 
   | Display name **(2)** | **miyagi-api**       |
   | Web service URL **(3)** | **<inject key="OpenAIEndpoint" enableCopy="true"/>**   |
   | Products **(4)** | **Unlimited** |
   | Click on  **(5)** | **Create** |

   ![](./Media/img-10-01-01.png)

1. Once the **HTTP API** is created, select **miyagi-api** **(1)** API from the list, select **Settings** **(2)**, scroll down to the **Subscription** section **Uncheck** **(3)** Subscription required and click on **Save** **(4)**.

   ![](./Media/miyagi-RR.png)

1. In the **miyagi-api**, select **Design** **(1)**, and click on **+  Add operation** **(2)** fill in the following details in **Frontend** and click on **Save** **(6)**.

   | **Parameter**           | **Values**                                            | 
   | ------------------------| ------------------------------------------------------| 
   | Display name **(3)**    | **completions**                                       | 
   | URL **(4)**             | from the drop-down select **Post**                    |
   | URL **(5)**             | in text box enter **/openai/deployments/<inject key="CompletionModel" enableCopy="false"/>/chat/completions**  |

   ![](./Media/opertation-completions.png)

1. Once the **completions** operation is created successfully, click on **+  Add operation** **(1)** fill in the following details in **Frontend** and click on **Save** **(6)**.

   | **Parameter**           | **Values**                                            | 
   | ------------------------| ------------------------------------------------------| 
   | Display name **(2)**    | **embeddings**                                       | 
   | Display name **(3)**    | **embeddings**                                          |
   | URL **(4)**             | from the drop-down select **Post**                    |
   | URL **(5)**             | in text box enter **/openai/deployments/<inject key="EmbeddingModel" enableCopy="false"/>/embeddings**  |

   ![](./Media/opertation-embeddings.png)

1. Once the **embeddings** operation is created successfully, click on the **Overview (1)** page, and copy the **Gateway URL (2)** Paste the Gateway URL into a notepad; you need this in the  upcoming task.

   ![](./Media/img-10-01-02.png)

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:

> - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

<validation step="d54f179b-7f83-4002-a3f5-d52f7c632b72" />
   
## Task 2: Update the Recommendation Service configuration to access Azure OpenAI through APIM

In this task, you will update the Recommendation Service configuration to access Azure OpenAI through API Management by modifying settings and implementing necessary authentication to enable seamless communication.

1. Navigate to Visual Studio Code, open the `appsettings.json` file from the path `miyagi\services\recommendation-service\dotnet\appsettings.json`.

      ![](./Media/lab3-t2-s1.png)

1. In the `appsettings.json` file, replace the **endpoint** value from **OpenAI resource endpoint** to **API Gateway URL**, which you copied in Task-1 Step-7, and press Ctrl + S to save the file.

      ![](./Media/lab3-t2-s2.png)

1. Open a new terminal by navigating to **miyagi/services/recommendation-service/dotnet** and right-click and, in the cascading menu, select **Open in Integrated Terminal**.

      ![](./Media/task4-1.png)

1. Run the following command to run the recommendation service locally

    ```
    dotnet build
    dotnet run
     ```

    > **Note**: Let the command run; meanwhile, you can proceed with the next step.

1. Open another tab in Edge, in the browser window, paste the following link:

      ```
      http://localhost:5224/swagger/index.html 
      ```

   > **Note**: Refresh the page continuously until you get the Swagger page for the recommendation service as depicted in the image below.

   ![](./Media/miyagi2.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at labs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="d1631c75-22e6-4fcc-a09d-c037ab0c0eb5" />

## Task 3: Verify that the Recommendation Service accesses Azure OpenAI through APIM

In this task, you will verify that the Recommendation Service successfully accesses Azure OpenAI through API Management by testing the API calls and ensuring that responses are correctly received and processed.

1. Navigate back to **Visual Studio Code**. In the **Miyagi (1)** folder, open the **ui/typescript (2)** folder and then open the **.env** file. Replace the existing value for **NEXT_PUBLIC_RECOMMENDATION_SERVICE_URL** with the URL provided below, and save the file.

   ```
   http://localhost:5224
   ```

   ![](./Media/lab2-11.png)

1. Open a new terminal by navigating to **Miyagi** and right-click on **ui/typescript** , in cascading menu select **Open in Integrated Terminal**.

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

   > **Note**: Refresh the page continuously until the Miyagi app runs locally as depicted in the image below.
                       
   ![](./Media/b1.png)

   > **Note:** If you encounter any pop-up error, close it and proceed to the next step.

1. On the **Personalize** page, select your **financial advisor** from the drop-down, and click on **Personalize**.

   ![](./Media/financial-advisor.png)  

1. You should see the recommendations from the **Recommendation Service** in the **Top Stocks** widget

   ![](./Media/financial-advisor-output.png) 

1. Navigate to the **Visual Studio Code**, and select the **dotnet** terminal, and you can go through the logs.

   ![](./Media/recommend-log.png)

1. From the Terminal, select **Node** terminal, press **Ctrl + C** to stop the recommendation service UI.

## Summary
 
In this lab, you have accomplished the following:

- Verified the API Management Service and created an API successfully.
- Updated the Recommendation Service configuration for Azure OpenAI access.
- Verified that the Recommendation Service successfully accesses Azure OpenAI.

### You have successfully completed the lab
