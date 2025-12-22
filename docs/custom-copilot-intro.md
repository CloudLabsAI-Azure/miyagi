# Build Custom Copilot Application using Microsoft Foundry

## Overall Estimated Duration: 60 Minutes

## Overview

In this lab, you will explore how to use Chat Copilot with your own data, leveraging Azure AI Search and Azure OpenAI Service. You will begin by retrieving necessary service values from the Azure portal and setting up the Chat Copilot app locally. Through configuring the app and uploading documents, you’ll enable the generation of context-based responses with citations for validation. This lab offers hands-on experience in integrating your data with Chat Copilot, managing documents, and interacting with the application for personalized insights.

## Objectives

Understand how to configure and run the Chat Copilot application locally, integrate your own documents, and generate AI-powered responses with contextual validation. By the end of this lab, you will be able to:

- **Run the Chat Copilot App Locally:** This exercise focuses on retrieving Azure OpenAI Service values, cloning the Chat-Copilot GitHub repository, setting up the environment with required dependencies, and running the Chat Copilot application locally for testing and interaction.

- **Chat with your own documents:** This exercise demonstrates how to upload and manage documents within the Chat Copilot application. You will interact with the chat interface to query the uploaded files, receive AI-generated responses, and validate them through citations for accuracy.
  
## Pre-requisites

Participants should have the following prerequisites

- **Basic Knowledge of Azure Services**: Familiarity with Azure OpenAI Service and Azure AI Search.
- **Experience with Git and Repositories**: Ability to clone and work with GitHub repositories.
- **Basic Programming Skills**: Proficiency in setting up environments and running applications locally.
- **Development Tools Knowledge:** Familiarity with Visual Studio Code, Node.js, .NET SDK, and package managers like Yarn/Chocolatey.
- **Understanding of AI Concepts:** Awareness of language models, embeddings, and how AI can interact with documents.

## Architecture

The architecture integrates **Azure OpenAI Service**, **Azure AI Search**, and the **Chat Copilot application** to provide personalized responses based on user-uploaded documents. Documents are uploaded to the Chat Copilot app, indexed by Azure AI Search, and used to generate context-aware responses through Azure OpenAI's language models. The application is run locally, pulling configuration values from the Azure portal and leveraging pre-built components from a GitHub repository. This setup enables seamless interaction with your data, providing accurate responses enriched with citations for validation.

## Architecture Diagram

  ![](../docs/labs/02-build-your-own-copilot/Media/n26.PNG)

## Explanation of Components

The architecture for this lab involves several key components:

- **Azure OpenAI Service**: Provides access to powerful AI models for natural language understanding and response generation.
- **Azure AI Search**: Enables indexing and searching through uploaded documents to support contextual responses.
- **Chat Copilot App**: A sample application that integrates Azure OpenAI and AI Search to generate insights and citations based on your data.
- **GitHub Repository**: Contains the source code and dependencies for configuring and running the Chat Copilot app locally.

## Getting Started with the Lab

## Accessing Your Lab Environment
 
Once you're ready to dive in, your virtual machine and **Guide** will be right at your fingertips within your web browser.

![](../docs/labs/02-build-your-own-copilot/Media/new/vm.png)

## Virtual Machine & Lab Guide
 
Your virtual machine is your workhorse throughout the workshop. The lab guide is your roadmap to success.
 
## Exploring Your Lab Resources
 
To get a better understanding of your lab resources and credentials, navigate to the **Environment** tab.
 
![](../docs/labs/02-build-your-own-copilot/Media/new/env2.png)
 
## Utilizing the Split Window Feature
 
For convenience, you can open the lab guide in a separate window by selecting the **Split Window** button from the Top right corner.
 
![](../docs/labs/02-build-your-own-copilot/Media/new/split.png)

## Managing Your Virtual Machine
 
Feel free to **Start**, **Stop**, or **Restart** your virtual machine as needed from the **Resources** tab. Your experience is in your hands!
 
![](../docs/labs/02-build-your-own-copilot/Media/new/res.png)

## Lab Guide Zoom In/Zoom Out
 
To adjust the zoom level for the environment page, click the **A↕ : 100%** icon located next to the timer in the lab environment.

![](../docs/labs/02-build-your-own-copilot/Media/new/zoom.png)

## Login to the Azure Portal

1. In the **Lab VM**, click on the **Azure portal** shortcut of the Microsoft Edge browser, which is created on the desktop.

   ![](../docs/labs/02-build-your-own-copilot/Media/new/azure.png)

1. On the Sign in to Microsoft Azure tab, you will see the login screen. Enter the following email/username, and click on **Next (2)**:
 
   - **Email/Username:** <inject key="AzureAdUserEmail"></inject> **(1)**

     ![](../docs/labs/02-build-your-own-copilot/Media/new/email.png)
     
1. Now enter the following temporary password and click on **Sign in (2)**.
 
   - **Temporary Access Pass:** <inject key="AzureAdUserPassword"></inject> **(1)**

     ![](../docs/labs/02-build-your-own-copilot/Media/new/pass.png)
   
1. If you see the pop-up **Stay Signed in?**, select **No**.

   ![](../docs/labs/02-build-your-own-copilot/Media/new/stay.png)

1. If a **Welcome to Microsoft Azure** popup window appears, select **Cancel** to skip the tour.

    ![](../docs/labs/02-build-your-own-copilot/Media/miyagi-image5.png)
   
1. Now that you will see the Azure Portal Dashboard, click on **Resource groups** from the Navigate panel to see the resource groups.

   ![](../docs/labs/02-build-your-own-copilot/Media/miyagi-image6.png)

1. In the **Resource groups**, click on **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** resource group.

   ![](../docs/labs/02-build-your-own-copilot/Media/br-1.png)

1. In the **miyagi-rg-<inject key="DeploymentID" enableCopy="false"/>** resource groups, verify the resources present in it.

   ![](../docs/labs/02-build-your-own-copilot/dec2025-build-custom-copilot-1.png)

   > [!IMPORTANT]<br>
   > **For a smoother experience during the hands-on lab, it's important to thoroughly review both the instructions and the accompanying notes. This will help you navigate through the tasks with ease and confidence.**

## Support Contact

The CloudLabs support team is available 24/7, 365 days a year, via email and live chat to ensure seamless assistance at any time. We offer dedicated support channels tailored specifically for both learners and instructors, ensuring that all your needs are promptly and efficiently addressed.

Learner Support Contacts:

- Email Support: cloudlabs-support@spektrasystems.com.
- Live Chat Support: https://cloudlabs.ai/labs-support

Now, click on **Next >>** from the lower right corner to move on to the next page.

![](../docs/labs/02-build-your-own-copilot/Media/new/next.png)

## Happy Learning!!
