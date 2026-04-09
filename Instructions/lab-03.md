# Lab 3: Deploy and Run the HR/Payroll Copilot Application

### Estimated Duration: 120 Minutes

   ![](../media/copilot-overview.png "Technical design")

**Smart Agent: At the heart of the solution is the Python object Smart_Agent. The agent has the following components:**

  - **Goals/Tasks:** Smart_Agent is given a persona and instructions to follow to achieve certain goals; for example, HR Copilot is about helping answer HR/Payroll questions and update employees' personal information. This is done using instructions specified in the system message.

  - **NLP interaction and tool execution:** For the ability to use multiple tools and functions to accomplish business tasks, the function calling capability of the 0613 version is utilized to intelligently select the right function (validate identity, search the knowledge base, update address, create ticket) based on the agent's judgment of what needs to be done. The agent is also able to engage with users by following the instructions and goals defined in the system message.

  - **Memory:** The agent maintains a memory of the conversation history. The memory is backed by Streamlit's session state.
  - **LLM:** The agent is linked to a 0613 GPT-4 model to power its intelligence.

## Lab objectives

You will be able to complete the following tasks:

- **Task 1:** Build your own HR/Payroll copilot locally
- **Task 2:** Integrate Azure Cognitive Search with your Application
- **Task 3:** Deploy the HR/Payroll Copilot application to Azure
    
### Task 1: Build your own HR/Payroll copilot locally

1. In the LabVM, open File Explorer, navigate to the below-mentioned path, right-click on the `secrets.env` file, and select **Open with Code**.

   ```
   C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot
   ```

    ![](../media/img38.png)

    > **Note:** If prompted with **Do you want to allow untrusted files in this workspace?**, select **Open**.

2. The Visual Studio code is opened on the desktop. Edit the below code and update the **Azure OpenAI Key**, **Embedding Model name and GPT Deployment name**, **Azure OpenAI Endpoint**, **Cognitive Search Endpoint**,and **AZURE_SEARCH_ADMIN_KEY** values that you have copied and stored in the text file earlier.

   | **Variables**                | **Values**                                                    |
   | ---------------------------- |---------------------------------------------------------------|
   | **AZURE_OPENAI_CHAT_DEPLOYMENT**          |  Replace the value with your **YOUR_GPT_MODEL** name that is **copilot-gpt**         |      
   | **AZURE_OPENAI_EMB_DEPLOYMENT**          |  Replace the value with your **YOUR_EMBEDDING_MODEL** name that is **CompletionModel**   |
   | **AZURE_OPENAI_ENDPOINT**          | **<inject key="OpenAIEndpoint" enableCopy="true"/>**          |
   | **AZURE_OPENAI_API_KEY**           | **<inject key="OpenAIKey" enableCopy="true"/>**               |
   | **AZURE_SEARCH_SERVICE_ENDPOINT**  | **<inject key="SearchServiceuri" enableCopy="true"/>**        |
   | **AZURE_SEARCH_ADMIN_KEY**         | **<inject key="SearchAPIkey" enableCopy="true"/>**            |

      > **Note:** If you're unable to see the full **Values** section in the table, click on the three dots (ellipsis) in the top right corner of your browser and try reducing the zoom level for better visibility.
   
      ![](../media/zoom.png)

3. After updating values, the `secrets.env` file should be as shown in the below screenshot. Press **CTRL + S** to save the file.

    ![](../media/img39.png)

4. To run the application from the command line, navigate to Command Prompt and run the below commands:

    ![](../media/cmdpr.png)

      ```
      cd C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot\employee_support
      ```

      ```
      streamlit run hr_copilot.py
      ```

5. Once the execution of `streamlit run hr_copilot.py` is completed, a locally hosted HR Copliot application will be opened in the web browser. 

   ![](../media/img17.png)

   ![](../media/img18.png)

6. Run the following query to validate the identity of the employee:

   ```
   John 1234
   ```

   ![](../media/img19.png)

7. Enter an example question such as `When will I receive the W2 form?`. The questions are answered by the Copilot by searching a knowledge base.

   ![](../media/L3-T1-S7.png)

8. Copilot can help update employee information, like address updates. For other information update requests, Copilot will log a ticket to the HR team to update the information. Enter `I moved to 123 Main St., San Jose, CA 95112, please update my address` in the HR Copilot app.

    ![](../media/L3-T1-S8.png)

      > **Note:** The copilot output may vary from what is shown in the screenshot.

9. Navigate back to **CMD** and stop the terminal by typing **ctrl + C**.

### Task 2: Integrate Azure Cognitive Search with your Application

<!--1. In the **Azure Portal**, search for **Storage accounts (1)** and select **Storage accounts (2)** from the services. 

    ![](../media/stsr.png)

2. From the **Storage account** page, select **copilotstorage<inject key="Deployment ID" enableCopy="false"/>**.

    ![](../media/img75.png)

3. From the left menu, select **Access keys (2)** under **Security + networking (1)** section. Click on **Show** and  Copy the **Connection string (3)** and store it in a text file for later use.

    ![](../media/stakeys.png)
-->

1. Navigate back to the **Azure portal**, then locate and select **AI Search (1)** from the left menu and click on **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (2)**.

   ![](../media/asr.png "Azure OpenAI")

1. On the **Overview (1)** page, click on **Import data (2)**.

    ![](../media/ipdta.png)

1.  Select **Azure Blob storage** as the **Data source**.

    ![](../media/abs.png)

1. On **What scenario are you targeting?** page select **Keyword search**.

    ![](../media/ks.png)

1. On the **Connect to your data** tab, provide the following details and click on **Next (6)**.

   | Settings| value|
   |---|---|
   |Subscription| **Default value** **(1)**|
   |Storage account| **copilotstorage<inject key="Deployment ID" enableCopy="false"/>** **(2)**|   
   |Blob Container name| **data (3)**|
   |Blob folder| **data (4)**|
   |Parsing mode| **JSON array** **(5)**|

    ![](../media/casb.png)

1. On the **Enrich your data (Optional)** tab, leave the default and click on **Next**.

    ![](../media/aien.png)

1. Next, on the **Preview mappings** tab, for the **id** field click on **3 dots (1)** and **delete (2)** it. 

   ![](../media/idel.png)

1. Next, on the **contentVector** field, click on the **Eclipse (1)** button in the right corner and select **Configure field (2)**.

    ![](../media/cvcf.png)

1. On the **Configure vector field** tab, set the **Type** as ``Collection(Edm.Single)`` **(1)** and **Dimensions** property to `1536` **(2)** and Click on **Create** **(3)** under **No vector search profiles**.

    ![](../media/din.png)

1. On the **Vector profile** tab, Click on **Create** under **No algorithm configurations**.

    ![](../media/nac.png)

1. On the **Vector algorithm** tab, leave the defaults and click on **Save**.

    ![](../media/vas.png)

1. On the **Vector profile** tab, select the **algorithm (1)** created in the previous step and Click on **Create (2)** under **No vectorizers**.

    ![](../media/nvcr.png)

1. On the **Vector algorithm** tab, leave the default and select the Azure OpenAI service as **Copilot-OpenAI-<inject key="Deployment ID" enableCopy="false"/>** **(1)** and model deployment as **CompletionModel (2)**. Click on **Save (3)**.

    ![](../media/svmod.png)

1. On the **Vector profile** tab, select the **Vectorizers (1)** created in the previous step and Click on **Save (2)**.

    ![](../media/vcsv.png)

1. On the **Configure vector field** tab, **check the boxes (1)** keep the **Dimensions** property to `1536` **(2)** and **Vector profile (3)** created in previous step and Click on **Save (4)**. 

    ![](../media/cfsv.png)
    
    > **Note**: If you are unable to save the **Configure Vector Field**, try deleting the **ContentVector** field. Then, recreate the field with the name **ContentVector** and select **Collection.single** for the **ContentVector** field and reperform from step 8 to step 15.

1. Click on **Next** after saving the above settings.

    ![](../media/nxtset.png)

1. On the **Advanced ranking and relevancy** tab keep the defaults and click on **Next**. 

    ![](../media/advrn.png)

18. Enter the **Objects name prefix** as ``payroll-hr`` **(1)**, and click on **Create (2)**.

    ![](../media/phrcr.png)

1. Once the **Create gets succeeded** you can click on **Go to Search explorer** to view the configurations and close it by clicking on **X** on the top right corner and then click **close**.

    >**Note:** It may take a few minutes before data is available in the Search explorer.

    ![](../media/csuc.png)

    ![](../media/xcor.png)

19. Now again from the Search service **Overview** page, click on **Add index (1)** dropdown and select **Add index (2)**.

    ![](../media/adin.png)

20. Now for the default **id field (1)** check the boxes mentioned in screenshot.Click on **+ Add field (2)**, and create ``search_query``, ``gpt_response``, ``search_query_vector`` fields with the configurations as provided in the below image.

    ![](../media/sq.png) 

    ![](../media/aldo.png)

21. Right click on the **search_query_vector (1)** field, and click on **Edit field (2)**.

    ![](../media/aqved.png)

24. On the **Configure vector field** tab, set **Type** as **Collection(Edm.Single) (1)**, set the **Dimensions** property to `1536` **(2)** and Click on **Create** **(3)** under **No vector search profiles**.

      ![](../media/edmsf.png)

12. On the **Vector profile** tab, Click on **Create** under **No algorithm configurations**.

    ![](../media/nac.png)

13. On the **Vector algorithm** tab, leave the defaults and click on **Save**.

    ![](../media/vas.png)

14. On the **Vector profile** tab, select the **algorithm (1)** created in the previous step and Click on **Create (2)** under **No vectorizers**.

    ![](../media/nvcr.png)

15. On the **Vector algorithm** tab, leave the default and select the Azure OpenAI service as **Copilot-OpenAI-<inject key="Deployment ID" enableCopy="false"/>** **(1)** and model deployment as **CompletionModel (2)**. Click on **Save (3)**.

    ![](../media/svmod.png)

16. On the **Vector profile** tab, select the **Vectorizers (1)** created in the previous step and Click on **Save (2)**.

    ![](../media/vcsv.png)

30. On the **Configure vector field** tab, **check the boxes (1)**, keep the **Dimensions** property to `1536` **(2)** and **Vector profile (3)** created in previous step and Click on **Save (4)**.

    ![](../media/sqv.png)

31. Enter the **Index name** as ``payroll-hr-cache`` **(1)**, and click on **Create**.

    ![](../media/phrc.png)

32. Navigate to the **Indexes (2)** tab under the **Search management (1)** section to view the **newly created indexes (3)**, copy the index names, and save them in a text editor for later use.

      ![](../media/indxxs.png)

33. From the left menu under **Settings (1)** Click on **Keys (2)** from the left menu, copy the **Primary admin key (3)**, and store them in a text file for later use.

    ![](../media/pak.png)

34. In the LabVM, open File Explorer, navigate to the below-mentioned path, right-click on the `secrets.env` file, and select **Open with Code**.

    ```
    C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot
    ```
   
    ![](../media/img38.png)

35. The Visual Studio code is opened on the desktop. Replace the following values and press **CTRL + S** to save the file.

     - **USE_AZCS**="**True**" #Set the value to true
     - **AZURE_SEARCH_INDEX_NAME**="YOUR_SEARCH_INDEX_NAME #Replace the value with the index name
     - **CACHE_INDEX_NAME**="YOUR_SEARCH_INDEX_NAME" #Replace the value with the cache index name
     - **AZURE_SEARCH_ADMIN_KEY**="YOUR_SEARCH_INDEX_NAME_KEY" #Replace the value with the primary admin key
 
36. In the LabVM, navigate to Desktop and search for `cmd` **(1)** in the search box, then click on **Command Prompt (2)**.

    ![](../media/cmdpr.png)

37. Run the below command to change the directory and run the HR Copilot application using the search service.

    ```bash
    cd C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot\employee_support
    ```

    ```
    streamlit run hr_copilot.py
    ```

38. Run the following query to validate the identity of the employee:
   
      ```
      john 1234
      ```

    ![](../media/img91.png)


39. Enter an example question such as `When will I receive the W2 form?`. The questions are now answered by the Copilot by searching a knowledge base. You can review this by navigating back to the command prompt and viewing the output.

    >**Note:** Because of indexing delays, the output may differ from what is shown in the screenshot. Please try running the prompt again.

    > **Note:** If you faced any issues while providing the above input, please try to run the command **pip install azure-search-documents==11.4.0b9** in the vs code at the file location and again try to perform from the step 35.

    ![](../media/img92.png)

40. Navigate back to **CMD** and stop the terminal by typing **ctrl + C**.

### Task 3: Deploy the HR/Payroll Copilot application to Azure

1. In the LabVM, open File Explorer, navigate to the below-mentioned path, right-click on the `main.bicep` file, and select **Open with Code**.

      ```
      C:\LabFiles\OpenAIWorkshop\infra
      ```

    ![](../media/img41.png)

2. In the **appsettings** section of the `main.bicep` file, replace the values below with the ones you copied previously in the text editor. Next, press **CTRL + S** to save the file.

   | **Variables**                     | **Values**                                                    |
   | --------------------------------- |---------------------------------------------------------------|
   | **AZURE_OPENAI_API_KEY**          | **<inject key="OpenAIKey" enableCopy="true"/>**               |
   | **AZURE_OPENAI_ENDPOINT**         | **<inject key="OpenAIEndpoint" enableCopy="true"/>**          |
   | **AZURE_OPENAI_EMB_DEPLOYMENT**   |  Replace the value with your **YOUR_EMBEDDING_MODEL** named as ``CompletionModel``    |
   | **AZURE_OPENAI_CHAT_DEPLOYMENT**  |  Replace the value with your **YOUR_GPT_MODEL** named as ``copilot-gpt``          |
   | **AZURE_SEARCH_SERVICE_ENDPOINT** | **<inject key="SearchServiceuri" enableCopy="true"/>**        |
   | **AZURE_SEARCH_INDEX_NAME**        | ``payroll-hr``                                               |
   | **AZURE_SEARCH_ADMIN_KEY**        | **<inject key="SearchAPIkey" enableCopy="true"/>**            |


   ![](../media/bcp.png)

   > **Note:** If you're unable to see the full **Values** section in the table, click on the three dots (ellipsis) in the top right corner of your browser and try reducing the zoom level for better visibility.
   
   ![](../media/zoom.png)

4. In the LabVM, navigate to Desktop and search for `cmd` in the search box, then click on **Command Prompt**.

    ![](../media/cmdpr.png)

5. Run the below command to change the directory.

   ```bash
   cd C:\LabFiles\OpenAIWorkshop
   ```

6. Run the below command to **Authenticate with Azure**. It will redirect you to the Azure-authorized website. Next, select your account and navigate back to Command Prompt.

   ```bash
   azd auth login
   ```

7. Run the below command to set up the resource group deployment and **Create a new environment**. Make sure to replace `{DeploymentId}` with **<inject key="Deployment ID" enableCopy="true"/>** in the below command.

   ```bash
   azd config set alpha.resourceGroupDeployments on
   ```
   
   ```bash
   azd env new copilot-{DeploymentId}
   ```

8. Run the below command to provision Azure resources and deploy your project with a single command.

   ```bash
   azd up
   ```
   
9. Please select your Azure subscription to use, enter `1`, and click on the **Enter** button.

   ![](../media/img29.png)

    >**Note:** If prompted to select an Azure location to use, select the location as **<inject key="Region" enableCopy="false"/>** location, and click on the **Enter** button. You can change the location using the up and down arrows.

11. Next, select **copilot-openai-<inject key="Deployment ID" enableCopy="False"/>** resource group and hit **ENTER**.

    ![](../media/rgter.png)

12. Once the deployment succeeds, you will see the following message **SUCCESS: Your application was provisioned and deployed to Azure**. The deployment might take **10-15 minutes**. It is producing a web package file, then creating the resource and publishing the package to the app service.

    ![](../media/terdon.png)

13. Navigate back to the Azure portal, search for **App services (1)** , and select **App services (2)**. Select the available **web app (3)** that you have deployed in the previous step.

    ![](../media/asrvs.png)

    ![](../media/apweb.png)

14. Next, click on **Browse** to open your Web application.

    ![](../media/brow.png)

    ![](../media/img46.png)

    > **Note:** If an issue occurs when you try to launch the app service, please restart the app service and wait five minutes before trying to launch the app again.

    > **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
 
    - Hit the Validate button for the corresponding task. If you receive a success message, you can proceed to the next task.
    - If not, carefully read the error message and retry the step, following the instructions in the lab guide.
    - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.

   <validation step="e563f609-c163-48c7-816f-e11985cba271" />

### Summary

In this lab, you have built your own HR/Payroll copilot locally ,integrated Azure Cognitive Search with your Application and deployed the HR/Payroll Copilot application to Azure.


