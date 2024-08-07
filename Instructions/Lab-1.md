# Lab 1: Getting Started with Building a Chat Application

### Estimated Duration: 30 minutes

In this exercise, you will be setting up the Open AI resource and installing the application locally.

## Lab objectives
In this lab, you will complete the following tasks:

- Task 1: Create an OpenAI resource and model **(Read-Only)**
- Task 2: Building a ChatGPT-like application on Streamlit with streaming

## Exercise 1: Open AI Setup and Installation of Applications

### Task 1: Create an OpenAI resource and model **(Read-Only)**

# READ-ONLY

 > **Note:** This task is **READ-ONLY**. The OpenAI setup is already configured for your environment.

1. In the Azure portal, search for **Azure OpenAI** **(1)** in the top search box, then select **Azure OpenAI** **(2)** under services.

   ![](../media/img1.png "Azure OpenAI")
   
1. From the **Cognitive Services | Azure OpenAI** pane, click on **Create**.

   ![](../media/img2.png "Azure OpenAI")
   
1. In the **Create Azure OpenAI** pane under the **Basics** tab, select the default subscription and select the existing **copilot-openai-<inject key="Deployment ID" enableCopy="false"/>** resource group. Select **East US** as Region, enter Name as **copilot-openai-<inject key="Deployment ID" enableCopy="false"/>** and select **Standard S0** for Pricing Tier. Click on **Next**.

   ![](../media/L1-T1-S3.png "Azure OpenAI")
   
1. Leave default settings for the Network and Tags tabs and click on **Next**.

1. Verify that validation has passed in the **Review + Submit** pane, and then click on **Create**.
     > **Note:** This task is **READ-ONLY**. The OpenAI setup is already configured for your environment. Please **DO NOT** click on **Create**. 

   ![](../media/L1-T1-S5.png "Azure OpenAI")
   
1. Deployment will take 5 minutes to complete. Once the deployment is successful, click on **Go to Resource**.

   ![](../media/L1-T1-S6.png "Azure OpenAI")
   
1. In the Azure OpenAI resource pane, select **Go to Azure OpenAI Studio**.

   ![](../media/L1-T1-S7.png "Azure OpenAI")
   
1. After navigating to Azure AI Studio, click on **Explore the new experience** pop-up on the top.

   ![](../media/explore_new-exp.jpg)

1. Click on **Deployments (1)** from the left navigation pane, click on **+ Deploy model** , select **Deploy base Model (2)**.  

   ![](../media/deploy-1.jpg)

1. In the **Select a model** window, select **gpt-4(1)** and click on **Confirm (2)**.

   ![](../media/new11.png)
   
1. On the **Deploy Model** tab, enter the following details and click on **Create (5)**.

    - **Deployment name**: copilot-gpt (1) 
    - **Model version**: 0613 (Default) (2)
    - **Deployment type**: Standard (3)
    - **Tokens per Minute Rate Limit (thousands)**: 15K (4)
    - **Enable dynamic quota**: Enabled (5)
    - Click on **Deploy** (6)

     ![](../media/new9.png)
   
### Task 2: Building a ChatGPT-like application on Streamlit with streaming  

1. In the Azure portal, search for **Azure OpenAI** **(1)** in the top search box, then select **Azure OpenAI** **(2)** under services.

   ![](../media/img1.png "Azure OpenAI")

1. From the **Azure AI Services | Azure OpenAI** pane, select **Copilot-OpenAI-<inject key="Deployment ID" enableCopy="false"/>**.

   ![](../media/select-openai.png "Azure OpenAI")

1. In the Azure OpenAI resource pane, select **Go to Azure OpenAI Studio**.

   ![](../media/L1-T1-S7.png "Azure OpenAI")
      
1. In the **Azure OpenAI Studio**, select **Deployments** under Management and verify that the **gpt-4** and **text-embedding-ada-002** models are present with the deployment names as **copilot-gpt** and **text-embedding-ada-002**. Review that the model's capacity is set to **15K TPM**. Copy the Azure OpenAI deployment names and model names into the text file for later use.
   
   ![](../media/new10.png)

1. Navigate back to the Azure OpenAI resource on the **Azure portal**, select **Key & Endpoint (1)** from the left menu, and click on **Show Keys (2)**. Copy the **KEY 1 (3)** and **Endpoint (4)**, and store them in a text file for later use.

   ![](../media/l1-t2-s5.png "Azure OpenAI")
   
1. Navigate back to **Azure OpenAI**, select **AI search (1)** from the left menu, and click on **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (2)**.

   ![](../media/l1-t2-s6.png "Azure OpenAI")

1. From the Overview tab of Cognitive Search, copy the **URL** and paste it into a text editor for later use.

   ![](../media/img36.png "Azure OpenAI")

1. From the left menu, select **Key (1)**, copy the **Primary admin key (2)**, and paste it into a text editor for later use.

   ![](../media/img66.png "Azure OpenAI")

1. In the LabVM, open File Explorer, navigate to the below-mentioned path, right-click on the `secrets.env` file, and select open with  **Visual Studio Code**.

   ```
   C:\LabFiles\OpenAIWorkshop\scenarios\incubations\copilot\ChatGPT
   ```

    ![](../media/img67.png)

1. In the `secrets.env` file, replace the following values with the ones you copied earlier. Press **CTRL+S** to save the file.

   | **Variables**                | **Values**                                                    |
   | ---------------------------- |---------------------------------------------------------------|
   | **AZURE_OPENAI_API_KEY**     | **<inject key="OpenAIKey" enableCopy="true"/>**               |
   | **AZURE_OPENAI_CHAT_DEPLOYMENT** | Replace with your **GPT** model Azure OpenAI Deployment Name  | 
   | **AZURE_OPENAI_ENDPOINT**    | **<inject key="OpenAIEndpoint" enableCopy="true"/>**          |

      ![](../media/img68.png)

1. Navigate back to File Explorer and open `chatgpt.py` with **Visual Studio Code** to view the code to build a ChatGPT-like app.

    ![](../media/img70.png) 
 
1. Next, click on the **Eclipse Button** on the top, then select **Terminal** and click on **New Terminal**.

    ![](../media/img69.png) 

1. Run the below command in the terminal to change the directory.

   ```
   cd C:\LabFiles\OpenAIWorkshop\scenarios\incubations\copilot\ChatGPT
   ```
   
1. To run the application from the command line, navigate back to Command Prompt and run the below command:

   > **Note**: You can enter your email address below to get notifications. If not, please leave this field blank and click on **Enter**.

   ```
   streamlit run chatgpt.py
   ```
   
1. Once the execution of `streamlit run chatgpt.py` is completed, a locally hosted demo application will be opened in the web browser.

   ![](../media/img71.png "Azure OpenAI")
   
   ![](../media/img72.png "Azure OpenAI")

1. Explore the app by running a few queries. Congratulations! You've built your own ChatGPT-like app in 50 lines of code.

   ![](../media/img73.png "Azure OpenAI")

   > **Note**: You may get a different response. please note chatgpt uses LLM and responses may vary everytime.
  
1. Navigate back to **VS Code** and stop the terminal by typing **ctrl + C**.

1. Click the **Next** button located in the bottom right corner of this lab guide to continue with the next exercise.

## Summary

In this exercise, you have created an OpenAI resource and model and built a ChatGPT-like application on Streamlit with streaming.

### You have successfully completed the lab
