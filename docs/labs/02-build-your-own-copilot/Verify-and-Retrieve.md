# Lab 1: Verify and Retrieve the values of Azure Resources (optional)

### Estimated Duration: 20 minutes

In this lab, you will verify and retrieve specific values such as Endpoint, Connection String, and Key for various Azure resources. This is crucial for ensuring the proper configuration and connectivity of these resources.

- Azure OpenAI : **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>** 
- Azure Cosmos DB account : **cosmos-<inject key="DeploymentID" enableCopy="false"/>**
- Search Service : **acs-<inject key="DeploymentID" enableCopy="false"/>**

1. To verify the deployment model names for "**deploymentOrModelId**" and "**embeddingDeploymentOrModelId**" follow the below steps:
   
      - On the Azure Portal home page, click on **Resource groups** in the **Navigate** panel.

          ![](./Media/miyagi-image6.png)
        
      - From the Resource groups page, click on **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**.

         ![](./Media/L1S1-ii.png)

      - In the **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>**, from the **Overview (1)** tab, select the **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>** **(2)**.

        ![](./Media/L1S1-iii.png)

      - In the **OpenAI Overview** page, click on **Go to Azure AI Foundry portal** it will navigate to **Azure AI Foundry portal**

         ![](./Media/aks-01.png)
   
      - In the **Azure AI Foundry portal**, from the left navigation pane under the **Shared resources** section, select **Deployments**.

           ![](./Media/deployments-11.png)
        
      - In the **Deployments**  **(1)** blade of Azure AI Foundry, click on **miyagi-CompletionModel-<inject key="DeploymentID" enableCopy="false"/>** deployment name and verify the **deployment name** of gpt-4.1 model **(2)**.

          ![](./Media/completionmodelnew.png)
        
          ![](./Media/miyagi-compl.png)
      
      -  Navigate back to the **Deployment (1)** page.

      - In the Deployments blade of Azure AI Foundry, click on **miyagi-EmbeddingModel-<inject key="DeploymentID" enableCopy="false"/>** deployment name and verify the **deployment name** of **text-embedding-ada-002 model (2)**.
        
         ![](./Media/deployments0909.png)

         ![](./Media/miyagi-embedded.png)

1. To verify the values for "**endpoint**" and "**apiKey**" follow the below steps:

   -  Navigate back to the **Azure portal**. 

   -  In the **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>** blade under **Resource Management** section, select **Keys and Endpoint (1)**, verify the **KEY 1 (2)** and **Endpoint (3)**.
     
      ![](./Media/L1S2-i.png)

1. To verify the values for  "**azureCognitiveSearchEndpoint**", "**azureCognitiveSearchApiKey**", follow below steps:
   
   - Navigate back to **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** resource group.

   - On the **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** page, select **acs-<inject key="DeploymentID" enableCopy="false"/>** from resources list.

      ![](./Media/miyagi-image110.png)
 
   - On **acs-<inject key="DeploymentID" enableCopy="false"/>** blade, verify the **URL**.
   
      ![](./Media/L1S3-iii.png)

   - On **acs-<inject key="DeploymentID" enableCopy="false"/>** blade, under **Settings** section, select **Key (1)** and  verify the **Primary admin Key (2)** value.
   
      ![](./Media/miyagi-image112.png)

1. To verify the values for "**cosmosDbUri**" and "**cosmosDbName**," please follow the steps below:

   - Navigative back to resource group **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** resource group page, select **cosmos-<inject key="DeploymentID" enableCopy="false"/>** from resources list.

     ![](./Media/miyagi-image113.png)
     
   - On **cosmos-<inject key="DeploymentID" enableCopy="false"/>** , verify the **URL**.
     
     ![](./Media/L1S4-ii.png)

   - On **cosmos-<inject key="DeploymentID" enableCopy="false"/>** under **Settings**, select **Keys** **(1)** and verify the value of the **Cosmos DB Primary Connection String** **(2)**.

     ![](./Media/L1S4-iii.png)

1. To obtain the values for "**blobServiceUri**", please follow the steps below:

   - Navigative back to resource group **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** resource group page, select **miyagiblobstorge<inject key="DeploymentID" enableCopy="false"/>** from resources list.

     ![](./Media/L1S5-i.png)

   - In the **miyagiblobstorge<inject key="DeploymentID" enableCopy="false"/>** storage account from the left menu select **Endpoints** **(1)** under **Settings** section verify the **Blob service** **(2)** under Blob service.

     ![](./Media/miyagi-image117.png)

## Summary
In this lab, you will verify and retrieve configuration values such as Endpoint, Connection String, and Key for various Azure resources like OpenAI Service, Cosmos DB, and Cognitive Search. This ensures proper configuration and connectivity. The steps involve accessing the Azure Portal, navigating to specific resource groups, and verifying the required values.

### Now click on **Next** from the lower right corner to move to the next page.

![](./Media/next-page.png)