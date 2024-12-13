# Lab 1: Getting Started with Building a Chat Application

### Estimated Duration: 30 minutes

Building a chat application involves designing the user interface for seamless communication, implementing backend services for real-time message handling, and integrating with databases for storing chat histories, while ensuring robust security and scalability to handle user interactions effectively.In this lab, you will be setting up the Open AI resource and installing the application locally.

## Lab objectives

In this lab, you will complete the following tasks:

- Task 1: Create an OpenAI resource and model **(READ-ONLY)**
- Task 2: Building a ChatGPT-like application on Streamlit with streaming

### Task 1: Create an OpenAI resource and model **(READ-ONLY)**

**Azure OpenAI**: Azure OpenAI Service is a cloud-based platform that provides access to OpenAI’s powerful language models, including GPT-4, GPT-3.5, Codex, and DALL-E12. This service allows developers to integrate these models into their applications for tasks such as content generation, summarization, semantic search, and natural language to code translation3.

Refer to the link for more information. [Azure OpenAI](https://learn.microsoft.com/en-us/azure/ai-services/openai/overview)

In this task, you will learn to create an Azure OpenAI resource in the Azure portal, configure its settings, and deploy the GPT-4 model in Azure AI Studio. This involves setting up the resource, navigating to Azure AI Studio, and specifying model deployment details.

> **Note:** This task is **READ-ONLY**. The OpenAI setup is already configured for your environment.

1. In the Azure portal, search for **OpenAI** **(1)** in the top search box, then select **Azure OpenAI** **(2)** under services.

   ![](../media/openai8.png "Azure OpenAI")

1. On the Azure AI Services page, select **Azure OpenAI (1)** from the menu on the left, then click **Create (2)**. button to start the process of setting up a new Azure OpenAI resource.

   ![](../media/openai_create1.png "Azure OpenAI")

1. In the **Create Azure OpenAI** pane under the **Basics** tab, Configure the details for your new resource, such as selecting the subscription, resource group, region and other required details.

   | Setting        | Value                                                                   |
   | -------------- | ----------------------------------------------------------------------- |
   | Subscription   | Default (1)                                                             |
   | Resource group | **copilot-openai-<inject key="Deployment ID" enableCopy="false"/>** (2) |
   | Region         | **East US** (3)                                                         |
   | Name           | **copilot-openai-<inject key="Deployment ID" enableCopy="false"/>** (4) |
   | Pricing Tier   | **Standard S0** (5)                                                     |

   ![](../media/L1-T1-S3.png "Azure OpenAI")

1. Accept the default settings for the Network and Tags tabs without making any changes. Click on **Next** to continue to the next step in the creation process.

1. In the **Review + Submit** pane, ensure that all validation checks have passed. After confirming that there are no errors, click on the **Create** button to finalize and start the deployment of your Azure OpenAI resource.

   > **Note:** This task is **READ-ONLY**. The OpenAI setup is already configured for your environment. Please **DO NOT** click on **Create**.

   ![](../media/L1-T1-S5.png "Azure OpenAI")

1. The deployment process will take approximately 5 minutes to complete. Once it’s finished, click on **Go to Resource** to access and manage your newly created Azure OpenAI resource.

   ![](../media/L1-T1-S6.png "Azure OpenAI")

1. In the Azure OpenAI resource pane, click on **Go to Azure AI Foundry portal** to navigate to the Azure AI Studio, where you can further configure and use your OpenAI models.

   ![](../media/L1-T1-S7-1.png "Azure OpenAI")

1. In the prompt titled **Discover an even better Azure AI Studio experience**, click **Close**.

   ![](../media/pop-upclose.png)

1. In the left navigation pane, click on **Deployments (1)**, then click on **+ Deploy model** **(2)**. Select **Deploy base Model** from the options presented.

   ![](../media/deploy-1-1.png)

1. In the **Select a model** window, choose **gpt-4 (1)** from the available options, and then click on **Confirm (2)** to proceed with the model selection.

   ![](../media/new11.png)

1. On the **Deploy Model** tab, input the required details such as Deployment name, Model version, Deployment type, Tokens per Minute Rate Limit, and enable dynamic quota. Once all fields are filled, Click on **Deploy** (6).

   | Setting                                  | Value                  |
   | ---------------------------------------- | ---------------------- |
   | Deployment name                          | **copilot-gpt (1)**    |
   | Model version                            | **0613 (Default) (2)** |
   | Deployment type                          | **Standard (3)**       |
   | Tokens per Minute Rate Limit (thousands) | **15K (4)**            |
   | Enable dynamic quota                     | **Enabled (5)**        |

   ![](../media/new9.png)

### Task 2: Building a ChatGPT-like application on Streamlit with streaming 

In this task, you will set up an Azure OpenAI resource, deploy models like GPT-4, and integrate the required API keys. After configuring the application with these details, you will run and test a ChatGPT-like app to verify its functionality, demonstrating how to use Azure OpenAI models in a practical application.

1. From your browser, open a new tab and navigate to [Azure AI Foundry portal](https://ai.azure.com/).

2. On **Azure AI Foundry** portal, click on **Sign in to get started** to sign in.

   ![](../media/aisimg1.png)

3. Once you are in Azure AI Studio's Sign in page, use the provided credentials to sign in.

   - **UserEmail**: <inject key="AzureAdUserEmail"></inject>

     ![](../media/aisimg2.png)

   - **Password**: <inject key="AzureAdUserPassword"></inject>

     ![](../media/aisimg3.png)

4. On the Azure AI Foundry pane, click on **+ Create project**.

   ![](../media/aisimg4.png)

5. In the **Create a project** page, provide **Project name** as **aiproject-<inject key="Deployment ID" enableCopy="false"/>** and click on **Customize**.

   ![](../media/aisimg5.png)

6. On **Create a hub** pane, provide details as follows, click on **Next (7)** and in the review pane, click on create.

   - **Hub name:** **aihub-<inject key="Deployment ID" enableCopy="false"/> (1)**

   - Leave **subscription** field as default **(2)**.

   - **Resource group:** **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (3)**

   - Leave **location** field as default **(4)**.

   - **Connect Azure AI Services or Azure openAI:** **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (5)**

   - **Connect Azure AI Search:** **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (6)**

     ![](../media/aisimg6.png)

7. Once the project is created, you will be in the project portal. Select **Open in management center**, now you'll be navigated to management portal.

   ![](../media/aisimg7.png)

8. In the management portal, select **Connected resources (1)** from left menu, select **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (2)** Azure OpenAI resource and use the **Copy (3)** option to copy the API Key. Note it down safely as you will be using this value further in this task.

   ![](../media/aisimg8.png)

9. Now in the same pane, click on **AzureAISearch**, the details page will be opened.

   ![](../media/aisimg9.png)

10. From the details pane, copy the **Target (1)** and **API Key (2)** values using the copy option. Note it down safely as you will be using this value further in this task.

    ![](../media/aisimg10.png)

11. In the LabVM, open File Explorer, navigate to the below-mentioned path, right-click on the `secrets.env` file, and select **Open with Code**.

    ```
    C:\LabFiles\OpenAIWorkshop\scenarios\incubations\copilot\ChatGPT
    ```

    ![](../media/img67.png)

12. In the `secrets.env` file, replace the following values. Press **CTRL+S** to save the file.

| **Variables**                    | **Values**                                                                  |
| -------------------------------- | --------------------------------------------------------------------------- |
| **AZURE_OPENAI_API_KEY**         | **<inject key="OpenAIKey" enableCopy="true"/>**                             |
| **AZURE_OPENAI_CHAT_DEPLOYMENT** | Replace the value with your **YOUR_GPT_MODEL** name that is **copilot-gpt** |
| **AZURE_OPENAI_ENDPOINT**        | **<inject key="OpenAIEndpoint" enableCopy="true"/>**                        |

![](../media/img68.png)

> **Note :** If you're unable to see the full **Values** section in the table, click on the three dots (ellipsis) in the top right corner of your browser and try reducing the zoom level for better visibility.

![](../media/zoom.png)

13. Navigate back to File Explorer and open `chatgpt.py` with **Visual Studio Code** to view the code to build a ChatGPT-like app.

    ![](../media/img70.png)

14. Next, click on the **Eclipse Button** at the top of the screen, then select **Terminal** from the dropdown menu and click on **New Terminal** to open a new terminal window.

    ![](../media/img69.png)

15. Run the following command in the terminal to change the directory:

    ```
    cd C:\LabFiles\OpenAIWorkshop\scenarios\incubations\copilot\ChatGPT
    ```

16. To run the application from the command line, enter the following command in the terminal:

    > **Note**: You can enter your email address below to get notifications. If not, please leave this field blank and click on **Enter**.

    ```
    streamlit run chatgpt.py
    ```

17. Once the command `streamlit run chatgpt.py` has executed, a demo application will be launched and opened in your web browser, hosted locally on your machine.

    ![](../media/img71.png "Azure OpenAI")

    ![](../media/img72.png "Azure OpenAI")

18. Explore the app by running a few queries. Congratulations! You've built your own ChatGPT-like application in 50 lines of code.

    ![](../media/img73.png "Azure OpenAI")

    > **Note**: You may get a different response. please note chatgpt uses LLM and responses may vary everytime.

19. Navigate back to **VS Code** and stop the terminal by typing **ctrl + C**.

20. Click the **Next** button located in the bottom right corner of this lab guide to continue with the next exercise.

## Summary

In this lab, you set up an Azure OpenAI resource and model, and built a ChatGPT-like application using Streamlit. You navigated the Azure portal to create and configure your OpenAI resource, verified model deployments, and gathered the necessary API keys and endpoints. After configuring your application with these details, you ran and tested it locally, successfully creating a functional ChatGPT-like app. This process demonstrated the integration of Azure OpenAI models into a practical application, showcasing the steps to build and deploy AI-driven chat functionalities.

### You have successfully completed the lab
