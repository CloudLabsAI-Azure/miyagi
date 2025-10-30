# Lab 4: Expose Open AI through APIM

### Duration: 60 minutes

In this lab, you'll delve into configuring and verifying APIs within Azure API Management, focusing on integrating the Azure OpenAI service. This entails setting up HTTP APIs, ensuring correct configuration, and obtaining a gateway URL for seamless external access and integration. You'll also explore policy creation, role definitions, and subscription management to securely operate the APIs. This lab underscores best practices in API management, ensuring robust authentication, authorization, and operational testing within Azure's comprehensive ecosystem.

## Lab objectives

You will be able to complete the following tasks:

- Task 1: Verify the deployed API Management service and create an API
- Task 2: Create API Management Policy and Roles
- Task 3: Update the Docker Image for the Recommendation service
- Task 4: Revision of Recommendation service from AKS
- Task 5: Setup Event Hub Logging and Validate Input

### Task 1: Verify the deployed API Management service and create an API

In this task, you'll be setting up an HTTP API within Azure API Management to interact with the Azure OpenAI service. It ensures the API is configured correctly and provides a gateway URL for external access and integration with other services.

1. Navigate to Azure portal, open the **Resource Group** named **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** and select **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service from the resources list.

   ![](./Media/miyagi-image54.png)

1. In the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service, click on **APIs** **(1)** under APIs from the left menu and select **HTTP** **(2)** under **Define a new API** to create an HTTP API.

    ![](./Media/api-01.png)

1. On the **Create an HTTP API** pane, enter the following values:
   
   | **Parameter**        | **Values**           | 
   | -------------------- | -------------------- | 
   | API Type **(1)**     | **Basic**            | 
   | Display name **(2)** | **miyagi-api**       |
   | Name **(3)**         | **miyagi-api**       |
   | Web service URL **(4)** | Enter the Endpoint of Azure OpenAI Endpoint  **<inject key="OpenAIEndpoint" enableCopy="true"/>**  |
   | API URL suffix **(5)** | **openai** |
   | Click on  **(6)** | **Create** |

   ![](./Media/miyagi-image56.png)

1. Once API is created, click on **Overview** **(1)** then copy the **Gateway URL** **(2)** of API Management service. Record the **URL** you require in the upcoming task.

    ![](./Media/L4T1S4.png)

   
> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task.
> - If you receive a success message, you can proceed to the next task. If not, carefully read the error message and retry the step, following the instructions in the labguide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

<validation step="5385328b-c6b7-4d03-9fcc-c2d33d96d9cd" />

### Task 2: Create API Management Policy and Roles

In this task, you'll be setting up API policies, defining roles and subscriptions, and integrating the Azure OpenAI Service API within Azure API Management. It ensures proper authentication, authorization, and operational testing of the API endpoints

1. In the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service, from the left navigation pane under **APIs** section select **APIs** **(1)**, click on the **three dots** **(2)** next to miyagi-api, select **Import** **(3)**, and click on **OpenAPI** **(4)**.

   ![](./Media/api-02.png)

   ![](./Media/api-03.png)

   ![](./Media/api-05.png)
   

1. In the popup of **Import from OpenAPI specification** paste the below link in the OpenAPI specification **textbox** **(1)** , and then click **import** **(2)**. 

   ```
   https://raw.githubusercontent.com/Azure/azure-rest-api-specs/main/specification/cognitiveservices/data-plane/AzureOpenAI/inference/stable/2023-05-15/inference.json
   ```

   ![](./Media/miyagi-image59.png)

1. You should now see a series of APIs under the **api-key**.
   
    ![](./Media/miyagi-image60.png)
   
1. In the **api-key** API navigate to the **Settings** **(1)** tab, and update the Web service URL **<inject key="OpenAIEndpoint" enableCopy="true"/>** **(2)**.

   ![](./Media/miyagi-image161n.png)

1. Scroll to the update the subscription key **Header Name** to **api-key** **(1)** and click on **Save** **(2)**.

   ![](./Media/miyagi-image61.png)

1. In the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service, from the left navigation pane under **APIs** click on **Products** **(1)** then select **+ Add** **(2)**.

   ![](./Media/api-06.png)

1. In the **Add product** window, specify **Display name** as **OpenAi** **(1)**, **Description** as **OpenAI** **(2)**. Under the **APIs** menu click the **Plus sign** **(3)** select the **Azure OpenAI Service API** **(4)** hit enter and click on **Create** **(5)**.

   ![](./Media/L4T2S7.png)

1. In the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service, from the left navigation pane under **APIs** select **Subscriptions** **(1)**  then lick on **+ Add subscription** **(2)**.

   ![](./Media/api-07.png)

1. In the **Add subscription** window, provide **Name** as **aoai-test** **(1)** and  **Display name** as **AOAI Test** **(2)**, and click on **Create** **(3)**.

   ![](./Media/miyagi-image64.png)

1. Once the subscription is **AOAI Test** created click the **three dots** **(1)** next to **AOAI Test** and then click **Show/hide keys** **(2)**. Copy the **Primary key** **(3)** key and save it for later.

   ![](./Media/miyagi-image(65).png)

1. Navigate to **Azure OpenAI** in the Azure Portal, select the **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**.

1. In the **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**, select **Access control (IAM)** **(1)**, click on **+ Add** **(2)**, and select **Add role assignment** **(3)**.

    ![](./Media/L4T2S12.png)
   
1. In the **Add role assignment** tab, search for **Cognitive Services User (1)** in the search bar, select **Cognitive Services User (2)**, and click on **Next (3)**.

    ![](./Media/apinew3.png)

1. In the **Members** tab, select **Managed identity** **(1)**, click on **+ Select Members** **(2)**.

    ![](./Media/miyagi-image82.png)

1. On the select managed identity pop up, for **Subscription (1)** accept default value then **Managed identity** select **API Management service** **(2)**, choose the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** **(3)**, then click-on **Select** **(4)**.

   ![](./Media/miyagi-image(68).png)

1. Click on **Next**.

1. In the **Review + assign** tab click on **Review + assign**.

1. Navigate back to **API Management service** in the Azure Portal, select the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service.
    
1. In the **API Management service**, select **APIs** **(1)**, select the **Azure OpenAI Service API** **(2)** API created in the earlier step, select **All Operations** **(3)** and click on **Policies </>** **(4)** under **Inbound processing**.

    ![](./Media/L4T2S19.png)

1. In the code editor copy the below policy to overwrite the **inbound** **(1)** tags only, replace **&lt;&lt;Azure_OpenAI_Endpoint&gt;&gt;** with **<inject key="OpenAIEndpoint" enableCopy="true"/>** **(2)** of API manager which you copied in Task 1 Step 4 and click on **Save** **(3)**.

      ```
      <inbound>
         <base />
         <set-header name="api-key" exists-action="delete" />
         <authentication-managed-identity resource="https://cognitiveservices.azure.com" output-token-variable-name="msi-access-token" ignore-error="false" />
         <set-header name="Authorization" exists-action="override">
            <value>@("Bearer " + (string)context.Variables["msi-access-token"])</value>
         </set-header>
         <set-backend-service base-url="<<Azure_OpenAI_Endpoint>>openai" />
      </inbound>
      ```

    ![](./Media/api-inbound1upd.png)

    >**Note**: Please ensure to paste the **OpenAIEndpoint** values and eliminate any duplication of **https://**.

1. In API Management, click on **Test** **(1)**, select Creates a **completion for the chat message** **(2)**, enter the gpt-4 deployment name **<inject key="CompletionModel" enableCopy="true"/>** **(3)** in the deployment-id field, enter **2024-08-01-preview** **(4)** in the API version field.

     ![](./Media/L4T2S21.png)

1. Scroll down to the **Request body** section **(1)**, replace the existing code with the code below, and click on **Send** **(2)**.

   ```
   {"model":"gpt-4","messages":[{"role":"user","content":"Hello! What does an API Management Service in Azure do?"}]}
   ```

   ![](./Media/new-api-body.png)

1. Scroll down the response and you should see a `200` response and a message back from your OpenAI service.

    ![](./Media/new-api-result.png)

### Task 3: Update the Docker Image for the Recommendation service

In this task, you'll be updating the configuration of the recommendation service, rebuilding the Docker image, pushing it to ACR, and ensuring that the updated image is ready for deployment within the Azure environment.

1. Navigate to Visual Studio Code, open **miyagi folder** and expand **services (1)/recommendation-service (2)/dotnet (3)** directory and select the **appsettings.json (4)**.

   ![](./Media/open-appsettings.png)

1. In the `appsettings.json` file, you have to replace the **endpoint** value from **OpenAI resource endpoint** with **API Gateway URL** which you have copied in Task-1 Step-4, **apiKey** value with the **subscription key** that was copied in Task-2 Step-9 and **Save** the file.

    ![](./Media/miyagi-image(72).png)

1. Navigate back to **Visual studio code** window and navigate to **miyagi folder** and expand **services (1)/recommendation-service (2)/dotnet (3)** right - click on dotnet in cascading menu, select **Open in integrated Terminal (4)**.

   ![](./Media/aks-04.png)

1. Now, you need to re-build the docker image for recommendation service by running the below docker command. Make to update the docker image name which was created earlier for recommendation service with the same name.

   ```
   docker build . -t miyagi-recommendation
   ```

    >**Note**: This command creates a Docker image named Miyagi-recommendation from the Dockerfile and associated files in the current directory.

1. Run the following command to ACR login.

    ```
    docker login <inject key="AcrLoginServer" enableCopy="true"/> -u <inject key="AcrUsername" enableCopy="true"/> -p <inject key="AcrPassword" enableCopy="true"/>
    ```

    >**Note**: The command **docker login <inject key="AcrLoginServer" enableCopy="false"/> -u <inject key="AcrUsername" enableCopy="false"/> -p <inject key="AcrPassword" enableCopy="false"/>** is used to authenticate your Docker client with the specified Azure Container Registry (ACR) using the provided username and password. This authentication is necessary for performing operations such as pushing and pulling container images to and from the ACR.

1. Run the following command to add the tag.

   ```
   docker tag miyagi-recommendation:latest <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest
   ```
   
   >**Note**: The command **docker tag miyagi-recommendation:latest <inject key="AcrLoginServer" enableCopy="false"/>/miyagi-recommendation:latest** tags a local Docker image with a new name that includes the Azure Container Registry (ACR) name. By tagging the image this way, you prepare it to be pushed to the specified Azure Container Registry.

1. Once you are logged into ACR. Run the below command to push the updated docker image of the recommendation service to the container registry.

   ```
   docker push <inject key="AcrLoginServer" enableCopy="true"/>/miyagi-recommendation:latest
   ```

   >**Note**: The command **docker push <inject key="AcrLoginServer" enableCopy="false"/>/miyagi-recommendation:latest** uploads the Docker image miyagi-recommendation:latest to the specified Azure Container Registry (ACR). This makes the image available in the ACR for use in deployments and other operations.
   
### Task 4: Revision of Recommendation service from AKS 

In this task, you'll be managing the deployment lifecycle of the recommendation service on Azure Kubernetes Service (AKS), including starting and stopping the service as well as verifying its functionality post-revision.

1. Navigate to the Azure portal, open the Resource Group named **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  and select **env-miyagi-<inject key="DeploymentID" enableCopy="false"/>** Kubernetes service from the resources list.

   ![](./Media/miyagi-image73.png)

1. In the Overview tab **env-miyagi-<inject key="DeploymentID" enableCopy="false"/>** Kubernetes service pane, click on **Stop** button  then click on **Yes**.

   ![](./Media/miyagi-image74.png)

   > **Note**: Wait till Kubernetes service is completely stopped. 

1. In the Overview tab **env-miyagi-<inject key="DeploymentID" enableCopy="false"/>** Kubernetes service pane, click on **Start** button.

   ![](./Media/miyagi-image75.png)

1. Once the Kubernetes service starts, select **Services and ingresses (1)** under **Kubernetes resources** and click on **External IP (2)** of the miyagi-recommendation-service.

   ![](./Media/miyagi-image76.png)

1. This will navigate a new tab with **miyagi-recommendation-service** web page.

   ![](./Media/miyagi-image77.png)

### Task 5: Setup Event Hub Logging and Validate Input

In this task, you'll be setting up Event Hub logging for API Management, configuring the necessary components in Azure, deploying the logging configuration using a Bicep template, and validating the integration through testing and monitoring.

1. In the **Azure portal**, Search and select **Event Hubs**, select the **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**.

    ![](./Media/api-product9.png)
   
1. In the **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>** Event hub Namespace tab, from the left menu select **Access control (IAM)** **(1)** , click on **+ Add** **(2)**, and select **Add role assignment** **(3)**.

   ![](./Media/L4T5S2.png)

1. In the **Add role assignment** tab, search for **Azure Event Hubs Data Sender (1)** in the search bar, select **Azure Event Hubs Data Sender (2)**, and click **Next (3)**.

   ![](./Media/miyagi-image80.png)

1. In the **Members** tab, select **Managed identity** **(1)**, click on **+ Select Members** **(2)**.

    ![](./Media/miyagi-image82.png)
 
1. On the select managed identity pop-up for **Subscription Accept the default (1)** under Managed identity drop-down select **API Management service** **(2)**, select the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** **(3)**, then click-on **Select** **(4)**.

   ![](./Media/miyagi-image(68).png)

1. Click on **Next**.

1. In the **Review + assign** tab, click on **Review + assign**.

   ![](./Media/namespace3.png)

1. On the **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, from the left-menu select **Event Hubs** **(1)** under **Entities** and click on **miyagi-event-<inject key="DeploymentID" enableCopy="false"/> (2)**

   ![](./Media/miyagi-image86.png)

1. In the **Event Hubs Instance** of **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**, from the left menu select **Shared access policies** **(1)** under **Settings**, click on **apimLoggerAccessPolicy** **(2)** and copy the **Primary connection string** **(3)** paste it in a notepad.

   ![](./Media/primaryconnectionstring.png)

1. Open the **notepad** from the jumpvm and copy and paste the below code, update the **&lt;&lt;API_MANAGEMENT_NAME&gt;&gt;** with **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** name and the **&lt;&lt;EVENT_HUB_CONNECTION_STRING&gt;&gt;** copied from the step above.

   ```
   resource existingApiManagement 'Microsoft.ApiManagement/service@2023-03-01-preview' existing = {
      name: '<<API_MANAGEMENT_NAME>>'
    }
    
    resource ehLoggerWithConnectionString 'Microsoft.ApiManagement/service/loggers@2023-05-01-preview' = {
      name: 'AOAILogger'
      parent: existingApiManagement
      properties: {
        loggerType: 'azureEventHub'
        description: 'Event hub logger with connection string'
        credentials: {
          connectionString: '<<EVENT_HUB_CONNECTION_STRING>>'
          name: 'ApimEventHub'
        }
      }
    }
   ```

   ![](./Media/miyagi-image121.png)

1. In the menu bar notepad select **Files** and click on **Save As**.

1. In the **Save As** navigate to the `C:\LabFiles\miyagi` **(1)** path, enter the file name **aoai-logger.bicep** **(2)**, Save as type to **All Files** **(3)** and click on **Save** **(4)**.

    ![](./Media/bicepfile2.png)

1. From the jumpvm open the PowerShell terminal and run the following command to log in to the **Azure portal**.

    ```
    az login
    ```

1. This will redirect to **Microsoft login page**, select your Azure account **<inject key="AzureAdUserEmail"></inject>**, and navigate back to the **PowerShell**.

    ![](./Media/azurelogin.png)

1. Run the following command to change the directory to `miyagi` root folder in the terminal and run the bicep file.
   
    ```
    cd C:\LabFiles\miyagi
    az deployment group create --resource-group <inject key="rgname" enableCopy="true"/> --template-file .\aoai-logger.bicep
    ```

    >**Note**: This command sequence navigates to the C:\LabFiles\miyagi directory containing the Bicep file and then deploys the resources defined in that file to the specified Azure resource group.

1. Navigate to Azure portal, open the Resource Group named **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**  and select **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service from the resources list.

    ![](./Media/lab3-t1-s1.png)

1. In the **miyagi-apim-<inject key="DeploymentID" enableCopy="false"/>** API Management service for the left menu, click on **APIs** **(1)** and  Select the **Azure OpenAI Service API** **(2)** created in the earlier step, select **All Operations** **(3)** and under **outbound proccessing** click on **Policies (4)** editor.

    ![](./Media/L4T5S17.png)

1. In the code editor copy the below policy to overwrite the **outbound (1)** tags only and click on **Save (2)**.

      ```
      <outbound>
         <base />
         <choose>
            <when condition="@(!context.Variables.GetValueOrDefault<bool>("isStream"))">
                  <log-to-eventhub logger-id="AOAILogger" partition-id="0">@{
                  var responseBody = context.Response.Body?.As<JObject>(true);
                  return new JObject(
                     new JProperty("prompt_tokens", responseBody["usage"]["prompt_tokens"].ToString()),
                     new JProperty("total_tokens", responseBody["usage"]["total_tokens"].ToString())
                  ).ToString();
            }</log-to-eventhub>
            </when>
         </choose>
      </outbound>
      ```

      ![](./Media/miyagi-image88.png)

1. Next open the **Miyagi UI** in a separate browser tab click **Personalize** and select your **Favorite Financial Advisor (1)** and choose **GPT-4 (2)** for the **Reasoning Engine** from the dropdown menu, then click on **Personalize (3)**. repeat the same step by selecting different **Favorite Financial Advisor** 6 - 7 times to generate additional logs.

    ![](./Media/miyagi-image126.png)

    >**Note**: Please ensure that the localhost is running in the VS code or else follow the steps in **Page 4 - Lab 2 - Task 4 - Steps 1 & 2**

1. Navigate back to Event Hub, select **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>** Event Hubs.

    ![](./Media/api-product9.png)

1. In the **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>** Event hub Namespace, from the left-menu select **Event Hubs** **(1)** under **Entity** and click on **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>**

    ![](./Media/miyagi-image89.png)

1. In the **miyagi-event-<inject key="DeploymentID" enableCopy="false"/>** Event hubs Instance, from the left menu select **Process data** **(1)**, scroll down till you find **Process your Event Hub data using Stream Analytics Query Language** and click **Start** **(2)**.

    ![](./Media/miyagi-image90.png)

1. Click on **Test Query** and in the Event Hub query, you should see log information for the tokens used.

    ![](./Media/miyagi-image91.png)

### Summary

In this lab, you configured an API Management service to manage APIs efficiently. Initially, the service was deployed, and an API was created within it. Subsequently, rules and roles were established to control access to the API. Event Hub logging was configured to monitor API usage effectively. Lastly, input validation was conducted to ensure the API handled various inputs correctly. Overall, this process ensured the effective management, security, and performance monitoring of the APIs, contributing to a well-organized and secure API ecosystem.

### You have successfully completed this lab. Now click on Next from the lower right corner to move to the next page.

![](./Media/next-page.png)
