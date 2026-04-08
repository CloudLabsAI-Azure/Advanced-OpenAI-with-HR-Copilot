# Lab 01: Getting Started with Building a Chat Application

## Overview

In this lab, you will learn how to build a chat application using Azure OpenAI. The lab involves setting up the necessary OpenAI resources and deploying a ChatGPT-like application using Streamlit. By the end of this lab, you will have a fully functional application that can interact with users through a simple web interface.

## Exercise 1: Open AI Setup and Installation of Applications

In this exercise, you will set up the OpenAI resource and install the necessary applications locally. This exercise is divided into two tasks: setting up the OpenAI resource (read-only) and building a ChatGPT-like application.

### Task 1: Create an OpenAI resource and model **(Read-Only)**

 > **Note:** This task is **READ-ONLY**. The OpenAI setup is already configured for your environment.

In this task, you will review the setup of the OpenAI resource, which has already been configured for your environment. This task is read-only, meaning no changes will be made.

1. In the Azure portal, search for **Azure OpenAI** **(1)** in the top search box, then select **Azure OpenAI** **(2)** under services.

   ![](../media/azoai.png "Azure OpenAI")
   
1. From the **Microsoft Foundry | Azure OpenAI** pane, click on **+ Create (1)**, from the drop-down, select **Azure OpenAI (2)**.

   ![](../media/crazaio.png "Azure OpenAI")
   
1. In the **Create Azure OpenAI** pane under the **Basics** tab, select the **default subscription (1)** and select the existing **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (2)** resource group. Select **East US (3)** as Region, enter Name as **copilot-openai-<inject key="Deployment ID" enableCopy="false"/>(4)** and select **Standard S0 (5)** for Pricing Tier. Click on **Next (6)**.

   ![](../media/nctcoa.png "Azure OpenAI")
   
1. Leave default settings for the Network and Tags tabs and click on **Next**.

1. Verify that validation has passed in the **Review + Submit** pane, and then click on **Create**.

     > **Note:** This task is **READ-ONLY**. The OpenAI setup is already configured for your environment. Please **DO NOT** click on **Create**. 

   ![](../media/rsc.png "Azure OpenAI")
   
1. The deployment might take approximately 5 minutes to complete. Once the deployment is successful, click on **Go to Resource**.

   ![](../media/gtr.png "Azure OpenAI")
   
1. In the Azure OpenAI resource pane, select **Go to Foundry portal**.

   ![](../media/gtfp.png "Azure OpenAI")
   
1. In the Azure OpenAI Studio, click **Deployments (1)**, click **+ Deploy model (2)** and select **Deploy base model (3)**.

   ![](../media/dbm.png)

1. On the **Select a Model** pane, search for `gpt-4.1` **(1)** and select **gpt-4.1 (2)** model from the list and click on **Confirm (3)**.

   ![](../media/gpt41.png)
   
1. On the **Deploy Model gpt-4.1** tab, enter the following details and click on **Deploy (4)**.

   - Deployment name: **copilot-gpt (1)**
   - Deployment type: **Standard (2)**
   - Tokens per Minute Rate Limit (thousands): **15K (3)**

     ![](../media/cogptdp2.png)
   
### Task 2: Building a ChatGPT-like application on Streamlit with streaming

In this task, you will configure a locally hosted application that mimics the functionality of ChatGPT. This will involve setting up necessary files, configuring secrets, and running the application. 

1. In the Azure portal, search for **Azure OpenAI** **(1)** in the top search box, then select **Azure OpenAI** **(2)** under services.

   ![](../media/azoai.png "Azure OpenAI")

1. From the **Microsoft Foundry | Azure OpenAI** pane, select **Copilot-OpenAI-<inject key="Deployment ID" enableCopy="false"/>**.

   ![](../media/opncoi.png "Azure OpenAI")

1. In the Azure OpenAI resource pane, select **Go to Foundry portal**.

   ![](../media/gtfp.png "Azure OpenAI")
      
1. In the **Microsoft Foundry** portal, select **Deployments (1)** under Management and verify that the **gpt-4.1** model are present with the deployment names as **copilot-gpt (2)**. Review that the model's capacity is set to **15K TPM (3)**. Copy the Azure OpenAI deployment names and model names into the text file for later use.
   
   ![](../media/dpl.png "Azure OpenAI")

   ![](../media/cap15.png)

   >**Note:** If you are not able to see the **capacity** value, please use the horizontal scroll bar from bottom of the page.

1. Navigate back to the Azure OpenAI resource on the **Azure portal**, from the left menu expand **Resource Management (1)** select **Keys & Endpoint (2)**. Copy the **KEY 1 (3)** and **Endpoint (4)**, and store them in a text file for later use.

   ![](../media/coke.png "Azure OpenAI")
   
1. In the LabVM, open File Explorer, navigate to the below-mentioned path, right-click on the `secrets.env` file, and select **Open with Code**.

   ```
   C:\LabFiles\OpenAIWorkshop\scenarios\incubations\copilot\ChatGPT
   ```

    ![](../media/img67.png)

1. In the `secrets.env` file, replace the following values. Press **CTRL+S** to save the file.

| **Variables**                    | **Values**                                                                  |
| -------------------------------- | --------------------------------------------------------------------------- |
| **AZURE_OPENAI_API_KEY**         | **<inject key="OpenAIKey" enableCopy="true"/>**                             |
| **AZURE_OPENAI_CHAT_DEPLOYMENT** | Replace the value with your **YOUR_GPT_MODEL** name that is **copilot-gpt** |
| **AZURE_OPENAI_ENDPOINT**        | **<inject key="OpenAIEndpoint" enableCopy="true"/>**                        |

   ![](../media/img68.png)

1. Navigate back to File Explorer and open `chatgpt.py` with **Visual Studio Code** to view the code to build a ChatGPT-like app.

    ![](../media/img70.png) 

    >**Tip:** **Streamlit** is an open-source Python framework that enables rapid development of interactive web apps for data science and machine learning projects. It allows developers to create user-friendly dashboards and visualizations with minimal coding.
 
1. Next, click on the **Eclipse Button** on the top, then select **Terminal** and click on **New Terminal**.

    ![](../media/img69.png) 

1. Run the below command in the terminal to change the directory.

   ```
   cd C:\LabFiles\OpenAIWorkshop\scenarios\incubations\copilot\ChatGPT
   ```

   > **Note**: If a **Do you trust the authors of the files in this folder?** pop-ups appears click on **Trust Workspace & Continue**.

    ![](../media/pi.png)

    ![](../media/pii.png)

1. To execute the application, run the following command.

   > **Note**: You can enter your email address below to get notifications. If not, please leave this field blank and click on **Enter**.

   ```
   streamlit run chatgpt.py
   ```
   
1. Once the execution of `streamlit run chatgpt.py` is completed, a locally hosted demo application will be opened in the web browser.

   ![](../media/img71.png "Azure OpenAI")
   
   ![](../media/img72.png "Azure OpenAI")

1. Explore the app by running a few queries. Congratulations! You've built your own ChatGPT-like app in 50 lines of code.

   >**Note:** The output may vary from what is shown in the screenshot.

   ![](../media/img73.png "Azure OpenAI")

1. Congratulations! You have successfully built your own ChatGPT-like application using Streamlit.

1. Navigate back to VS Code and stop the terminal by typing **Ctrl + C**.

## Summary

In this lab, you have accomplished the following:

- You reviewed the setup of the OpenAI resource, which was pre-configured for your environment.
- You configured and deployed a ChatGPT-like application using Streamlit.
- You successfully hosted the application locally and tested its functionality by running queries.
