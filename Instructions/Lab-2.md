# Lab 02: Understand function calling in Open AI GPT

## Overview

This lab focuses on the function calling feature in Azure OpenAI, an advanced capability that enables GPT-3 and GPT-4 models to produce structured JSON outputs tailored to specific functions. By integrating these models with external systems, you gain enhanced control and flexibility in automation and data processing tasks. Throughout this lab, you’ll explore the setup, configuration, and practical implementation of function calling within the Azure OpenAI environment, empowering you to leverage this powerful feature in real-world scenarios.

To know more about Azure function calling, please refer to [Function calling is now available in Azure OpenAI Service] (https://techcommunity.microsoft.com/t5/azure-ai-services-blog/function-calling-is-now-available-in-azure-openai-service/ba-p/3879241).

## Task 1: Understand Function calling

In this task, you will explore how to set up and configure the Azure OpenAI environment to leverage function calling. You will gather necessary information such as deployment names, API keys, and service endpoints and configure them in a sample project. Finally, you will run a Jupyter Notebook to observe how function calling works in action.

1. In the Azure portal, search for **Azure OpenAI** **(1)** in the top search box, then select **Azure OpenAI** **(2)** under services.

   ![](../media/img1.png "Azure OpenAI")

1. From the **Azure AI services | Azure OpenAI** pane, select **Copilot-OpenAI-<inject key="Deployment ID" enableCopy="false"/>**.

   ![](../media/select-openai.png "Azure OpenAI")

1. In the Azure OpenAI resource pane, select **Go to Azure OpenAI Studio**.

   ![](../media/L1-T1-S7.png "Azure OpenAI")
      
1. In the **Azure OpenAI Studio**, select **Deployments** under Management and verify that the **gpt-4** and **text-embedding-ada-002** models are present with the deployment names as **copilot-gpt** and **text-embedding-ada-002**. Review that the model's capacity is set to **15K TPM**. Copy the Azure OpenAI deployment names and model names into the text file for later use.
   
   ![](../media/p12.png "Azure OpenAI")

1. Navigate back to the Azure OpenAI resource on the **Azure portal**, select **Keys & Endpoint (1)** from the left menu, and click on **Show Keys (2)**. Copy the **KEY 1 (3)** and **Endpoint (4)**, and store them in a text file for later use.

   ![](../media/l1-t2-s5.png "Azure OpenAI")
   
1. Navigate back to **Azure OpenAI**, select **AI Search (1)** from the left menu, and click on **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (2)**.

   ![](../media/l1-t2-s6.png "Azure OpenAI")

1. From the Overview tab of Cognitive Search, copy the **URL** and paste it into a text editor for later use.

   ![](../media/img36.png "Azure OpenAI")

1. From the left menu, select **Keys (1)**, copy the **Primary admin key (2)**, and paste it into a text editor for later use.

   ![](../media/img66.png "Azure OpenAI")

1. Open **Visual Studio Code** from the desktop; next, click on **File** and select **Open Folder**.

    ![](../media/img55.png) 

2. Navigate to the below-mentioned path and click on **Select folder**. 

    ```
    C:\LabFiles\openai\Basic_Samples\Functions
    ```

   ![](../media/l2-t1-s2.png) 

4. On the **Do you trust the authors of the files in this folder?** pop-up check the box next to **Trust the authors of all files in the parent folder 'Basic_Samples'**, and select **Yes, I trust the authors**.

    ![](../media/img57.png) 

5. In the **Functions** folder, open `config.json` and replace the following values with the ones you copied earlier. Next, press **CTRL + S** to save the file.

    - **DEPLOYMENT_NAME**: `Replace the value with the gpt-model name`
    - **OPENAI_API_BASE**: `Replace the value with Azure OpenAI Endpoint`
    - **OPENAI_API_KEY**: `Replace the value with Azure OpenAI Key`
    - **SEARCH_SERVICE_ENDPOINT**: `Replace the value with the Search Service Endpoint`
    - **SEARCH_ADMIN_KEY**: `Replace the value with the Search Service key`

        ![](../media/img58.png) 

6. Next, click on the **Eclipse Button (1)** on the top, then select **Terminal (2)** and click on **New Terminal (3)**.

    ![](../media/img59.png) 

7. In the new terminal, run the following command to install the required modules:

    ```
    pip install -r requirements.txt
    ```
    
8. Once the requirements are installed, close the terminal.

9. Open the `working_with_functions.ipynb` file from the left menu.

    ![](../media/img60.png) 

10. Click on the **Run (1)** button in the first cell. Once the pop-up `Install/Enable suggested extensions Python + Jupyter` appears, click on it to install the Python and Jupyter extensions. 

    ![](../media/img61.png) 

11. Next, on the **Choose a Kernel source** pop-up, select **Python Environments**. This will initiate the installation of the extension.

       ![](../media/img62.png) 

12. Next, on the **Select a Python Environment** pop-up, select **Python 3.10.0**. This will set the Python Environment. 

       ![](../media/p24.png) 

    > **Note**: If prompt **Runnning cells with 'c:\pytjon311\python.exe' requires the ipykernel package.** then click on **Install**.

      ![](../media/install.png)

13. Execute the notebook cell by cell (using either `Ctrl + Enter` to stay on the same cell or `Shift + Enter` to advance to the next cell) and observe the results of each cell execution.

       ![](../media/openai1.1.png)

       > **Note:** Please ensure to run the notebook end to end and observe the output for each cell. 

#### Validation

<validation step="2945e6ae-9193-4560-b2b6-9b42f8bc7917" />

## Summary
- You have learned how to configure and set up the Azure OpenAI environment for function calls.
- You explored gathering and configuring essential details like deployment names, API keys, and service endpoints.
- You observed the function calling process through the execution of a Jupyter Notebook in Visual Studio Code.
