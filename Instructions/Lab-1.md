# Lab 1: Getting started with building Chat Application

## Exercise 1: Open AI setup and Installation of Application

In this exercise, you will be setting up the Open AI resource and installtion of application locally.

### Task 1: Create Open AI resource and model (Read-Only)

1. In the Azure portal, search for **Azure OpenAI** **(1)** in the top search box then select **Azure OpenAI** **(2)** under services.

   ![](../media/img1.png "Azure OpenAI")
   
1. From the **Cognitive Services | Azure OpenAI** pane, click on **Create**.

   ![](../media/img2.png "Azure OpenAI")
   
1. In the Create Azure OpenAI pane under Basics tab, select the default subscription and select the existing **sql-chat-gpt-<inject key="Deployment ID" enableCopy="false"/>** resource group. Select **East US** as Region, enter Name as **copiolt-openai-<inject key="Deployment ID" enableCopy="false"/>** and select **Standard S0** for Pricing tier. Click on **Next**

   ![](../media/img6.png "Azure OpenAI")
   
1. Leave default settings for Network and Tags tabs, click on **Next**.

1. In the Review + submit pane, verify that validation passed and then click on **Create**.

   ![](../media/img3.png "Azure OpenAI")
   
1. Deployment will take 5 minutes to complete. Once the deployments is succeeded, click on **Go to resource**.

   ![](../media/img4.png "Azure OpenAI")
   
1. In the Azure OpenAI resource pane, select **Go to Azure OpenAI Studio**.

   ![](../media/img5.png "Azure OpenAI")
   
1. In the Azure OpenAI Studio click **Deployment (1)** and click **+ Create new deployment (2)**.

   ![](../media/img7.png "Azure OpenAI")
   
1. On the **Deploy Model** tab enter the following details and click on **Create (5)**.

   - Select a model: **gpt-35-turbo (1)**
   - Model version: **Auto-update to default (2)**
   - Deployment name: **Copilot-model (3)**
   - Tokens per Minute Rate Limit (thousands): **15K (4)**

   ![](../media/img8.png "Azure OpenAI")
   
### Task 2: Building ChatGPT like application on Streamlit with streaming  

1. Navigate to OpenAI resource on **Azure portal**, click on **Go to Azure OpenAI Studio** it will navigate to **Azure AI Studio**.

   ![](../media/img14.png "Azure OpenAI")
      
1. In the **Azure AI Studio**, select **Deployments (1)** under Management and verify that **gpt-4** and **text-embedding-ada-002** **(2)** model is present with the deployment name as **copilot-gpt4** and **text-embedding-ada-002**, review that the capacity of the model is set to **15K TPM**. Copy the OpenAI Model names into the text file for later use.
   
   ![](../media/img34.png "Azure OpenAI")


2. select **Key & Endpoint (1)** from the left menu and click on **Show Keys (2)**. Copy the **KEY 1 (3)** and **Endpoint (4)**, store it in a text file for later use.

   ![](../media/img9.png "Azure OpenAI")

1. In the LabVM, navigate to Desktop and search for `cmd` in the search box then click on **Command Prompt**.
   
1. Run the below command to change the directory.

   ```
   cd C:\LabFiles\OpenAIWorkshop-Automation\scenarios\incubations\automating_analytics
   ```
   
1. Provide settings for Open AI and Database by creating a ```secrets.env``` file in the root of this folder by running the below command.

   ```
   code secrets.env
   ```
   
1. You will see the Visual Studio code is opened in the desktop. Enter the below code and update the OpenAI Key, Model Name and Endpoint values which you have copied and stored in text file earlier.

   ```
   AZURE_OPENAI_API_KEY="********************************" #Replace with the OpenAI Key
   AZURE_OPENAI_GPT4_DEPLOYMENT="NAME_OF_GPT_4_DEPLOYMENT" #Replace with the OpenAI Model Name
   AZURE_OPENAI_CHATGPT_DEPLOYMENT="NAME_OF_CHATGPT_4_DEPLOYMENT" #Replace with the OpenAI Model
   AZURE_OPENAI_ENDPOINT=https://openairesourcename.openai.azure.com/ #Replace with the OpenAI Endpoint
   SQL_ENGINE = "sqlite"
   ```
   
1. After updating values the `secrets.env` file should be as shown in the below screenshot, press **CTRL + S** to save the file.

   ![](../media/img10.png "Azure OpenAI")
   
1. To run the application from the command line navigate back to Command Prompt and run the below command:

   >**Note**: Here, you can enter your email address below to get notifications. Otherwise, leave this field blank and click on **Enter**.

   ```
   streamlit run app.py
   ```
   
1. Once the execution of `streamlit run app.py` is completed. A locally hosted demo appliation will be opened in the web browser. 

   ![](../media/img11.png "Azure OpenAI")
   
   ![](../media/img12.png "Azure OpenAI")
