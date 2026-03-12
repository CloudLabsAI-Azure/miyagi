# Lab 2: Explore and Verify the Containerized Recommendation service in Azure Container App using Local Miyagi UI

### Estimated Duration: 60 minutes

## Lab Scenario

In this lab, you will explore and verify the containerized Recommendation Service deployed in Azure Container Apps using the local Miyagi UI. Begin by configuring the Miyagi UI to connect to the Azure endpoint of the Recommendation Service. Next, test various API calls through the UI to ensure accurate recommendations based on user inputs. Document any discrepancies or issues encountered during testing. Finally, validate the overall integration and functionality of the services.

## Lab objectives

In this lab, you will complete the following tasks:

- Task 1: Verify the Recommendation service running in the Container App by Personalizing
- Task 2: Update Container App Recommendation service URL for Miyagi UI
- Task 3: Access Recommendation Service running on Azure Container Apps from Local Miyagi-UI

## Task 1: Verify the Recommendation service running in the Container App by Personalizing

In this task, you will verify the Recommendation service running in the Container App by personalizing recommendations based on user preferences and testing the service's responses.

1. Navigate back to container app **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>**, and click on **Log Stream** under **Monitoring** from the left menu.

    ![](./Media/img-13.png)
   
      ![](./Media/img-14.png)
   
     > **Note** : Please click on **Refresh** for the logs to show up .

1. Navigate back to **Miyagi Recommendations** page, scroll down to the **Recommendations**, click on **POST /personalize** expansion, and click on **Try it out**.

   ![](./Media/continer-recommendations.png)

1. Replace the provided **JSON code** below and click on **Execute**.

   ```
   {
       "userInfo": {
       "userId": "50",
       "riskLevel": "aggressive",
       "favoriteSubReddit": "finance",
       "favoriteAdvisor": "Jim Cramer"
       },
       "portfolio": [
           {
               "name": "Stocks",
               "allocation": 0.5
           },
           {
               "name": "Bonds",
               "allocation": 0.3
            },
            {
                    "name": "Cash",
                    "allocation": 0.1
            },
            {
                    "name": "HomeEquity",
                    "allocation": 0.1
            }
          ],
          "stocks": [
            {
                    "symbol": "MSFT",
                    "allocation": 0.3
            },
            {
                    "symbol": "ACN",
                    "allocation": 0.1
            },
            {
                    "symbol": "JPM",
                    "allocation": 0.3
            },
            {
                    "symbol": "PEP",
                    "allocation": 0.3
            }
       ]
   }
   ```

      ![](./Media/recomme-parameter-body.png)

1. In the **Miyagi Recommendations** page, scroll down to the Responses session review that it has been executed successfully by checking the code status is **200**, and review the **Response body** section.

   ![](./Media/recommendations-parameter-output.png)

   > **Note**: Please ignore the 500 error and move on to the next task.

1. Navigate back to container app **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>| Log stream**, review the **logs**.

## Task 2: Update Container App Recommendation service URL for Miyagi UI

In this task, you will update the Container App Recommendation service URL for the Miyagi UI by modifying the configuration settings to ensure seamless integration between the front end and the service.

1. Once you have completed the review of the logs, click on **Ingress** **(1)** under **Networking** and copy the **Endpoints** **(2)** URL link.

   ![](./Media/img-15.png)

1. Navigate back to **Visual Studio Code**, then go to **miyagi > ui\typescript > .env**. Replace the existing value for **NEXT_PUBLIC_RECOMMENDATION_SERVICE_URL** with the copied **Endpoints** value, and save the file.

   ![](./Media/cntr4.png)

## Task 3: Access Recommendation Service running on Azure Container Apps from Local Miyagi-UI 

In this task, you will access the Recommendation Service running on Azure Container Apps from your local Miyagi UI by configuring API endpoints and ensuring proper network connectivity.

1. Open a new terminal: by navigating  **miyagi/ui** and right-click on **ui/typescript** , in cascading menu select **Open in Integrated Terminal**.

   ![](./Media/image-rg-25.png)

1. Run the following command to install the dependencies
   
    ```
    yarn dev
    ```

   > **Note**: Let the command run; meanwhile, you can proceed with the next step.

1. Open another tab in Edge, and  browse the following

   ```
   http://localhost:4001
   ```

    > **Note**: Refresh the page continuously until you get the Miyagi app running locally as depicted in the image below.
                       
    ![](./Media/b1.png)

    > **Note:** If you encounter any pop-up error, close it and proceed to the next task.

1. In the to the **recommendation service** ui page, and click on **Personalize** button.

    ![](./Media/service-personalize.png)

1. In the **personalize** page, select your **financial advisor** from the drop-down, and click on **Personalize**.

   ![](./Media/financial-advisor.png)  

1. You should see the recommendations from the recommendation service in the Top Stocks widget.

   ![](./Media/financial-advisor-output.png)

1. Navigate back to the **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>** Container App, from the left-side menu select **Log stream** under Monitoring, and you can go through the logs.

    ![](./Media/img-16.png)

1. Navigate back to VS Code, from the Terminal select Node terminal, and press **Ctrl + C** to stop the recommendation service ui page.

## Summary

In this lab, you have accomplished the following:

- Verified the Recommendation Service by personalizing user interactions successfully.
- Updated the Recommendation Service URL in Miyagi UI configuration.
- Accessed the Recommendation Service from the local Miyagi UI effectively.

### You have successfully completed the lab

