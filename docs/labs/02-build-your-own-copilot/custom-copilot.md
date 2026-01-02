# Lab: Build Custom Copilot Application using Microsoft Foundry

## Estimated Duration: 60 Minutes

## Overview 

In this lab, you'll run Chat Copilot locally after retrieving Azure OpenAI Service values from the Azure portal. By cloning the Chat-Copilot GitHub repo and setting up dependencies, you'll configure and execute the application. Uploading documents enables interaction with Copilot, which generates responses based on their content, complete with citations for validation. This exercise provides hands-on experience in utilizing Chat Copilot with your own data, managing documents and sessions within the application.

## Objectives

- Exercise 1: Run the Chat Copilot App Locally

   - Task 1: Retrieving the Azure OpenAI Service values
   - Task 2: Cloning the Chat-Copilot GitHub Repo
   - Task 3: Setting up the Environment
   - Task 4: Configure and run the Chat Copilot App Locally

- Exercise 2: Chat with your own documents

   - Task 1: Chat with your own documents in the Chat Copilot Application

## Exercise 1: Run the Chat Copilot App Locally

In this exercise, you will run the Chat Copilot app locally by setting up the environment, installing dependencies, and launching the application for testing and interaction.

### Task 1: Retrieving the Azure OpenAI Service values

In this task, you will retrieve the Azure OpenAI Service values by accessing the service configuration, querying the API, and ensuring the correct integration of parameters for your application.

1. In the Azure Portal, search for **OpenAI (1)** and select **Azure OpenAI (2)**
   
    ![](./Media/dec2025-build-custom-copilot-3.png)

1. On the **Microsoft Foundry | Azure OpenAI** page, select the pre-created **Azure OpenAI** resource named **OpenAIService-<inject key="DeploymentID" enableCopy="false"/>**.

    ![](./Media/dec2025-build-custom-copilot-4.png)  

1. From the left navigation pane, expand **Resource Management (1)**, select **Keys and Endpoints (2)**. Copy **Key 1 (3)** and **Endpoint (4)**, then store them in Notepad.
   
    ![](./Media/new/1.png)

   > **Note**: If you don't see the left side navigation pane, click on the **Hamburger** icon in the top left corner.

   ![](./Media/lop-03.png)

1. From the **Overview (1)** page, click on **Go to Foundry portal (2)**.
   
    ![](./Media/dec2025-build-custom-copilot-6.png)

1. Go to **Deployments (1)** in the left navigation pane, click on the names of your AI model to copy them, and paste them into Notepad **(2)**.
    
   ![](./Media/new/2.png)

   > **Note**: Click on the **Expand** button, if you don't see the left side navigation pane.

     ![](./Media/dec2025-build-custom-copilot-8.png)     

### Task 2: Cloning the Chat-Copilot GitHub Repo

In this task, you will clone the Chat-Copilot GitHub repository by using Git commands to download the code to your local machine for further exploration and development.

1. In the LabVM, click on **Start**, from the start menu search for **Powershell (1)** and right click on **Windows PowerShell (2)** and then choose **Run as administrator (3)** to open PowerShell as an administrator.

    ![](./Media/dec2025-build-custom-copilot-9.png)  
   
1. Navigate to the directory `C:/Users/azureuser` by running the below command.
 
   ``` 
   cd C:/Users/azureuser
   ```
1. Run the command to clone the GitHub repository.
   
   ``` 
   git clone https://github.com/CloudLabsAI-Azure/chat-copilot CHAT-COPILOT
   ```

    ![](./Media/cp4.png)

1. Open **Visual Studio Code** from the **LabVM** Desktop.

   ![](./Media/new/3.png)

1. click on `File (1) > Open folder (2)`.

   ![](./Media/cp5.png)

1. Select **CHAT-COPILOT (1)** and click **Select folder (2)**.

   ![](./Media/cp6.png)

1. If the pop up appears for **Do you trust the authors of the file in this folder**, click on **Yes, I trust the authors.** 

    ![](./Media/cp7.png)

1. Review the files in the CHAT-COPILOT folder.

   ![](./Media/ch4.png)

   >**Note:** You can close any reommendations you get in the VS Code.
   >   ![](./Media/recom-0201.png)

### Task 3: Setting up the Environment

In this task, you will set up the environment for the Chat-Copilot project by installing necessary dependencies, configuring environment variables, and preparing the development environment for local execution.

1. In the LabVM, click on **Start**, from the start menu search for **Powershell (1)**, right click on **Windows PowerShell (2)** and run **PowerShell as an administrator (3)**.

   ![](./Media/br2.png)

1. Setup your environment by navigating to the scripts directory of chat-copilot using the command:

   ``` 
   cd C:\Users\azureuser\chat-copilot\scripts\
   ```

1. Run the below command to install Chocolatey, dotnet-7.0-sdk, nodejs, and yarn:

   ```
   .\Install.ps1
   ```

    ![](./Media/cp8.png)   

   >**Note:** If you receive an error that the script is not digitally signed or cannot execute on the system, you may need to change the execution policy or unblock the script.
 
   >**Note:** You can use the following command if you receive any error related to execution policy `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` and then rerun the above step. 

### Task 4: Configure and run the Chat Copilot App locally

In this task, you will configure and run the Chat Copilot app locally by setting up the environment, adjusting configuration files, and launching the application for testing and development.

1. Configure Chat Copilot by running the following command. You can use the Azure OpenAI Service Name, Key, Endpoint, and the already deployed model names that you noted down in the previous steps or use the values from the below mentioned table.
   
   ```
   .\Configure.ps1 -AIService {AI_SERVICE} -APIKey {API_KEY} -Endpoint {AZURE_OPENAI_ENDPOINT} -CompletionModel {DEPLOYMENT_NAME} -EmbeddingModel {DEPLOYMENT_NAME}
   ```
   | **Variables**                          | **Values**                                            |
   | ---------------------------------------| ------------------------------------------------------|
   | API_KEY                                | **<inject key="OpenAIKey" enableCopy="true"/>**       |
   | AI_SERVICE                             | **AzureOpenAI**| 
   | AZURE_OPENAI_ENDPOINT                  | **<inject key="OpenAIEndpoint" enableCopy="true"/>**  |
   | CompletionModel:{DEPLOYMENT_NAME}      | **<inject key="CompletionModel" enableCopy="true"/>** |
   | EmbeddingModel:{DEPLOYMENT_NAME}       | **<inject key="EmbeddingModel" enableCopy="true"/>**  |

   >**Note:** If a Security warning pop-up window appears, choose **Yes**.

     ![](./Media/new/4.png)

   >**Note:** The code should look similar to the image below:

     ![](./Media/cp9.png)

1. Run Chat Copilot locally. This step starts the **backend API** application. frontend
 
   ```powershell
   .\Start-Backend.ps1
   ```
   > **Note:** It may take a around 5 minutes for Yarn packages to install on the first run, wait untill the command run successfully.

     ![](./Media/new/5.png)
 
1. Once you get the **Build Succeeded** message in the above command, open another tab in **Edge**, in the browser window paste the following link, and you should see a confirmation message: `Healthy`.
 
   ```powershell
   http://localhost:40443/healthz
   ```
   > **Note:** Don't close the PowerShell window keep it running up.
  
     ![](./Media/data9.png)
    
1. In the LabVM, click on **Start**, from the start menu search for **PowerShell 7 (1)** and select for **PowerShell 7 (x64) (2)**.

   ![](./Media/cp10.png)
 
1. Run the following command to change the path.

   ```
   cd C:\Users\azureuser\chat-copilot\scripts\
   ```
 
1. Run the following to set the execution policy.
 
   ```
   Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope Process
   ```
 
1. The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose you to the security risks described in the about_Execution_Policies help topic. If prompted **Do you want to change the execution policy?,** enter **A** and hit **Enter**.
 
1. Configure **Chat Copilot** by running the following command.
 
   ```powershell
   .\Start-Frontend.ps1
   ```

    ![](./Media/cp11.png)   

     >**Note:** Please wait for 5-7 mins for the command to run completely. If it throws any warnings please ignore.     

1. Once the deployment of the script is executed successfully it will redirect to `http://localhost:3000/` Chat CoPilot in **Edge** browser.
 
   >**Note:** Please wait for 3-4 mins for the browser to load.
  
1. You will get an output similar to this for the frontend:

   ![azure](./Media/data11.png)

1. You will get an output similar to this for the backend:

   ![azure](./Media/data12.png)

>**Congratulations** on completing the Task! Now, it's time to validate it. Here are the steps:
> - Hit the Validate button for the corresponding task. If you receive a success message, you have successfully validated the lab. 
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com.

<validation step="df43cbbf-d05e-4a3b-b34a-a5f2dd969bad" />

## Exercise 2: Chat with your own documents

In this exercise, you will chat with your own documents by uploading files to the Chat Copilot app and interacting with the integrated chat interface for personalized responses.

### Task 1: Chat with your own documents in the Chat Copilot Application

In this task, you will learn how to chat with your own documents in the Chat Copilot application by uploading files, configuring the document processing, and interacting with the integrated chat interface for personalized responses.

1. Navigate back to the WebApp. Select **Documents (1)**  from the top menu bar, click on **Upload (2)** and select **+ New local chat document (3).**

    ![](./Media/new/6.png)  

1. Navigate to `C:\Labfiles\Documents` **(1)** to upload the three pdfs. Select the three files **(2)** and click **Open. (3)**

    ![](./Media/cp12.png)

1. Ensure the files are uploaded successfully before proceeding.

    ![](./Media/cp13.png)

1. Once it is uploaded, navigate to the **Chat (1)** tab then provide the below prompt **(2)** then click **send (3)** button and then check how the response is generated by Copilot.

    ```
    How to operate Android Auto in Porche Taycan? Give step-by-step instructions.
    ```
    ![](./Media/cp14.png)
   
1. Provide another prompt and check how the response is generated by Copilot.

    ```
    Give detailed information on Apple CarPlay.
    ```
    ![](./Media/ch13.png)

     >**Note**: If you get any error while sending the second prompt, related to exceeded Token rate limit. Please wait for 5-10 seconds, reload the webapp by pressing **F5** and then re-send the prompt.

      ![](./Media/cp15.png)     
   
1. The response not only answered the question based on the content found in these documents, but it also included **citations** to that content to validate the accuracy of the information. When you click on an annotation, the app jumps right to the page of the document that goes into the comparison of the plans, so that we can read more or do additional validation on the accuracy of the answer under the citation section.

1. Click on the **Edit** button on the left to rename.

    ![](./Media/new/7.png)

1. Give any name you prefer **(1)** and then click on right mark **(2)**.    

    ![](./Media/new/8.png)

## Summary

In this lab, you retrieved Azure OpenAI Service values, cloned the Chat-Copilot GitHub repository, set up the environment with required dependencies, ran the Chat Copilot app locally, and interacted with your documents within the app.

## Conclusion

By completing the Build Custom Copilot Application using Microsoft Foundry lab, you gained hands-on experience in setting up and running a Chat Copilot application locally. You explored Azure OpenAI Service integration, cloned and configured the Chat-Copilot repository, installed necessary dependencies, and executed the application. Additionally, you learned to upload documents and interact with them through Copilot, observing how AI-generated responses are derived and validated with citations. This lab enhanced your practical understanding of building AI-powered applications and managing document-driven interactions.

## You have successfully completed the lab
