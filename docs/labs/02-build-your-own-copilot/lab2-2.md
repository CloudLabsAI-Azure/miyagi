# Lab 2.2: Explore and Verify the Containerized Recommendation Service in the Azure Container App Using the Local Miyagi UI

In this lab, you'll be exploring and verifying the automated containerized recommendation service in the Azure Container App.
 
### Task 1: Verify the recommendation service running in the Container App by personalizing

1. In the Azure Portal page, in the Search resources, services, and docs (G+/) box at the top of the portal, enter **Container Apps (1)**, and then select **Container Apps (2)** under services.

   ![](./Media/container-app-select.png)

1. In the **Container Apps** blade, select **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>**.

   ![](./Media/container-ca-miyagi.png)

1. In the **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>** page, from the left navigation pane, select **Ingress** **(1)** under setting session and click on **Endpoints** **(2)** URL link.

   ![](./Media/container-ca-ingress.png)

1. Navigate back to the container app **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>**, and click on **Log Stream** under **Monitoring** from the left menu.

    ![](./Media/logstream.png)
   
      ![](./Media/containerapps-logsstream.png)
   
     > **Note**: Please click **Refresh** for the logs to show up.

1. Navigate back to the **Miyagi Recommendations** page, scroll down to the **Recommendations**, click on **POST/personalize** expansion, and click on **Try it out**.

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

1. On the **Miyagi Recommendations** page, scroll down to the Responses session, review that it has been executed successfully by checking that the status code is **200**, and examine the **Response body** section.

      ![](./Media/recommendations-parameter-output.png)


1. Navigate back to the container app **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>|Log stream** and review the **logs**.

### Task 2: Update Container App Recommendation service URL for Miyagi UI

1. Once you have completed the review of the logs, click on **Ingress** **(1)** under **Settings** and copy the **Endpoints** **(2)** URL link.

   ![](./Media/container-ca-ingress.png)

1. Navigate back to **Visual Studio Code**, navigate to **miyagi>ui>typescript>.env.**, and replace existing code for **NEXT_PUBLIC_RECCOMMENDATION_SERVICE_URL** with copied for **Endpoints**, and save the file. 

   ![](./Media/cntr4.png)

### Task 3: Access recommendation service running on Azure Container Apps from Local Miyagi-UI

1. Open a new terminal by navigating to **miyagi/ui** and right-clicking on **ui/typescript**. In the cascading menu, select **Open in intergate Terminal**.

   ![](./Media/image-rg-25.png)

1. Run the following command to install the dependencies:
   
    ```
    yarn dev
    ```

   **Note**: Let the command run; in the meantime, you can proceed with the next step.

1. Open another tab in Edge and  browse the following:

   ```
   http://localhost:4001
   ```

    > **Note**: Refresh the page continuously until you get the Miyagi app running locally, as depicted in the image below.
                       
   ![](./Media/miyagi1.png)

1. On the **recommendation service** UI page, click on **personalize** button.

    ![](./Media/service-personalize.png)

1. On the **personalize** page, select your **financial advisor** from the drop-down menu and click on **Personalize**.

   ![](./Media/financial-advisor.png)  

1. You should see the recommendations from the recommendation service in the Top Stocks widget.

   ![](./Media/financial-advisor-output.png)

1. Navigate back to the **ca-miyagi-rec-<inject key="DeploymentID" enableCopy="false"/>** Container App. From the left-side menu, select **Log stream** under Monitoring, and you can go through the logs.

    ![](./Media/continer-app-logstream.png)

    > **Note**: Navigate back to the VS code. From the Terminal, select Node terminal and press Ctrl + C to stop the recommendation service UI page. 
   

## Summary

In this lab, you have updated the Containerized Recommendation service endpoint in Miyagi UI and verified it locally.
