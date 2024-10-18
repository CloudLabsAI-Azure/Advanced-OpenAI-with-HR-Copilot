# Lab 03: Deploy and Run the HR/Payroll Copilot Application

   ![](../media/copilot-overview.png "Technical design")

**Smart Agent: At the heart of the solution is the Python object Smart_Agent. The agent has the following components:**

  - **Goals/Tasks:** Smart_Agent is given a persona and instructions to follow to achieve certain goals; for example, HR Copilot is about helping answer HR/Payroll questions and update employees' personal information. This is done using instructions specified in the system message.

  - **NLP interaction and tool execution:** For the ability to use multiple tools and functions to accomplish business tasks, the function calling capability of the 0613 version is utilized to intelligently select the right function (validate identity, search the knowledge base, update address, create ticket) based on the agent's judgment of what needs to be done. The agent is also able to engage with users by following the instructions and goals defined in the system message.

  - **Memory:** The agent maintains a memory of the conversation history. The memory is backed by Streamlit's session state.
  - **LLM:** The agent is linked to a 0613 GPT-4 model to power its intelligence.

    
### Task 1: Build your own HR/Payroll copilot locally

In this task, you will set up the HR/Payroll Copilot locally on your LabVM. You'll configure the application by updating necessary environment variables and running it using Streamlit. This task ensures you understand how to set up and run the application in a local environment before moving to Azure.

1. In the Azure portal, search for **Azure OpenAI** **(1)** in the top search box, then select **Azure OpenAI** **(2)** under services.

   ![](../media/L2-T1-S1.png "Azure OpenAI")

2. From the **Azure AI services | Azure OpenAI** pane, select **Copilot-OpenAI-<inject key="Deployment ID" enableCopy="false"/>**.

   ![](../media/L2-T1-S2.png "Azure OpenAI")

3. In the Azure OpenAI resource pane, select **Go to Azure OpenAI Studio**.

   ![](../media/L2-T1-S3.png "Azure OpenAI")
      
4. In the **Azure OpenAI Studio**, select **Deployments** under Management and verify that the **gpt-4** and **text-embedding-ada-002** models are present with the deployment names as **copilot-gpt** and **text-embedding-ada-002**. Review that the model's capacity is set to **15K TPM**. Copy the Azure OpenAI deployment names and model names into the text file for later use.
   
   ![](../media/L2-T1-S4.png "Azure OpenAI")

5. Navigate back to the Azure OpenAI resource on the **Azure portal**, select **Keys & Endpoint (1)** from the left menu, and click on **Show Keys (2)**. Copy the **KEY 1 (3)** and **Endpoint (4)**, and store them in a text file for later use.

   ![](../media/L2-T1-S5.png "Azure OpenAI")
   
6. Navigate back to **Azure OpenAI**, select **AI search (1)** from the left menu, and click on **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (2)**.

   ![](../media/l1-t2-s6.png "Azure OpenAI")

7. From the Overview tab of Cognitive Search, copy the **URL** and paste it into a text editor for later use.

   ![](../media/img36.png "Azure OpenAI")

8. From the left menu, select **Key (1)**, copy the **Primary admin key (2)**, and paste it into a text editor for later use.

   ![](../media/img66.png "Azure OpenAI")

9. In the LabVM, open File Explorer, navigate to the below-mentioned path, right-click on the `secrets.env` file, and select open with  **Visual Studio Code**.

   ```
   C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot
   ```

    ![](../media/img38.png)

10. The Visual Studio code is opened on the desktop. Edit the below code and update the **Azure OpenAI Key**, **Embedding Model name and GPT Deployment name**, **Azure OpenAI Endpoint**, **Cognitive Search Endpoint**, and **AZURE_SEARCH_ADMIN_KEY** values that you have copied and stored in the text file earlier.

    ```
      AZURE_OPENAI_API_KEY = "YOUR_OPENAI_KEY" //#Replace it with the OpenAI key you copied in Task 1,Step 5.
      AZURE_OPENAI_ENDPOINT= "YOUR_OPENAI_ENDPOINT" //#Replace with the OpenAI Endpoint you copied in Task 1,Step 5.
      AZURE_OPENAI_EMB_DEPLOYMENT = "YOUR_EMBEDDING_MODEL" //#Replace with the name of your embedding model deployment you copied in Task 1,Step 4.
      AZURE_OPENAI_CHAT_DEPLOYMENT= "YOUR_GPT_MODEL" //#Replace with the name of your Open AI Chat Deployment you copied in Task 1,Step 4.
      AZURE_SEARCH_SERVICE_ENDPOINT= "YOUR_SEARCH_SERVICE_ENDPOINT" //#Replace with Search Service Endpoint you copied in Task 1,Step 7.
      AZURE_SEARCH_ADMIN_KEY= "YOUR_SEARCH_SERVICE_ADMIN_KEY" //#Replace the value with the Primary admin key you copied in Task 1,Step 8.
    ```

11. After updating values, the `secrets.env` file should be as shown in the below screenshot. Press **CTRL + S** to save the file.

    ![](../media/L2-T1-S11.png)

12. Next, click on the **Eclipse Button** on the top, then select **Terminal** and click on **New Terminal**.

    ![](../media/img69.png) 

13. Run the below command in the terminal to change the directory.

    ```
    cd C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot\employee_support
    ```
   
14. To execute the application, run the following command.

   ```
   streamlit run hr_copilot.py
   ```

    > **Note**: You can enter your email address below to get notifications. If not, please leave this field blank and click on **Enter**.

15. Once the execution of `streamlit run hr_copilot.py` is completed, a locally hosted HR Copliot application will be opened in the web browser. 

    ![](../media/img17.png)

    ![](../media/img18.png)

16. Run the following query to validate the identity of the employee:

    ```
    John 1234
    ```

    ![](../media/img19.png)

17. Enter an example question such as `When will I receive the W2 form?`. The questions are answered by the Copilot by searching a knowledge base.

    ![](../media/L3-T1-S7.png)

18. Copilot can help update employee information, like address updates. For other information update requests, Copilot will log a ticket to the HR team to update the information. Enter `I moved to 123 Main St., San Jose, CA 95112, please update my address` in the HR Copilot app.

    ![](../media/L3-T1-S8.png)

19. Navigate back to **CMD** and stop the terminal by typing **ctrl + C**.

#### Validation

<validation step="bfc0e96d-c61e-4a91-b1ee-a10df581cdd5" />

### Task 2: Integrate Azure Cognitive Search with your Application

This task involves integrating Azure Cognitive Search with your HR/Payroll Copilot application. You'll set up data sources, configure the search index, and create vector profiles for enhanced search capabilities.

1. In the **Azure Portal**, search and select **Storage accounts**. 

    ![](../media/img74.png)

2. From the **Storage account** page, select **copilotstorage<inject key="Deployment ID" enableCopy="false"/>**.

    ![](../media/img75.png)

3. From the left menu, select **Access keys** under **Security + networking** section. Copy the **Connection string** and store it in a text file for later use.

    ![](../media/img76.png)

4. Next, navigate to **Azure AI services**, select **AI Search (1)** from the left menu, and click on **copilot-openai-<inject key="Deployment ID" enableCopy="false"/> (2)**.

   ![](../media/l1-t2-s6.png "Azure OpenAI")

5. On the **Overview (1)** page, click on **Import data (2)**.

    ![](../media/img77.png)

6.  Select **Azure Blob storage** as the **Data source**.

    ![](../media/img78.png)

7. On the **Connect to your data** tab, provide the following details and click on **Next: Add cognitive skills (Optional) (7)**.

   | Settings| value|
   |---|---|
   |Data source name| **copilotstorage<inject key="Deployment ID" enableCopy="false"/>** **(1)**|
   |Data to extract| **Content and metadata** **(2)**|
   |Parsing mode| **JSON array** **(3)**|
   |Connection string | **YOUR_STORAGE_ACCOUNT_CONNECTIONSTRING (4)**|
   |Container name| **data (5)**|
   |Blob folder| **data (6)**|

   ![](../media/L2-T2-S7.png)

8. On the **Add cognitive skills (optional)** tab, leave the default and click on **Skip to: Customize target index**.

9. Next, on the **Customize target index**  tab, enter the **Index name** as **payroll-hr (1)**. Set the values as provided in the below image (make sure you select `Collection(Edm.Single)` as the type for the content vector field).

   ![](../media/img81.png)

10. Next, on the **contentVector** field, click on the **Eclipse** button in the right corner and select **Configure vector field**.

      ![](../media/img82.png)

11. On the **Configure vector field** tab, set the **Dimensions** property to `1536` and Click on **Create** under No vector search profiles.

      ![](../media/vector1.png)

12. On the **Vector profile** tab, Click on **Create** under No algorithm configurations.

      ![](../media/vector2.png)

13. On the **Vector Algorithm** tab, leave the default and click on **Save**.

      ![](../media/vector3.png)

14. On the **Vector profile** tab, select the algorithm created in the previous step and Click on **Create** under No vectorizers.

      ![](../media/vector4.png)

15. On the **Vector algorithm** tab, leave it as the default and select the Azure OpenAI service as **Copilot-OpenAI-<inject key="Deployment ID" enableCopy="false"/>** and model deployment as **text-embedding-ada-002** . Click on **Save**.

      ![](../media/vector5.png)

16. On the **Vector profile** tab, select the Vectorizers created in the previous step and Click on **Create** under Compressions.

      ![](../media/vector6.png)

17. On the **Compressions** tab, leave the default and click on **Save**. 

      ![](../media/vector7.png)

18. In the **Vectore profile** tab, select Algorithm, Vectorizations, and Compressions recently created, and click on **Save**

      ![](../media/vector8.png)

19. On the **Configure vector field** tab, keep the **Dimensions** property to `1536` and **Vector profile** created in previous step and Click on **Save**. Click on **Next: Create an indexer**.

     ![](../media/vector9.png)

     > **Note**: If you are unable to save the **Configure Vector Field**, try deleting the **ContentVector** field. Then, recreate the field with the name **ContentVector** and select **Collection.single** for the **ContentVector** field and reperform from step 10 to step 19.
 
20. Enter the **Indexer name** as **payroll-hr**, and click on **Submit**.

      ![](../media/img84.png)

21. From the **Overview (1)** page, click on **Import data (2)** again.

       ![](../media/img77.png)

22. On the **Connect to your data** tab, select the existing data source and select the storage account then, click **Next: Add cognitive skills (optional)**.

      ![](../media/img85.png)

23. On the **Add cognitive skills (optional)** tab leave the default and click on **Skip to: Customize target index**.

24. Next, on the **Customize target index**  tab, enter the **Index name** as **payroll-hr-cache (1)**. Click on **+ Add field**, and create **id, search_query, search_query_vector, gpt_response** fields with the configurations as provided in the below image (make sure you select `Collection(Edm.Single)` as the type for the search_query_vector field).

      ![](../media/img86.png)

25. In the **search_query_vector** field, click on the **Eclipse** button in the right corner and select **Configure vector field**.

      ![](../media/img87.png)

26. On the **Configure vector field** tab, set the **Dimensions** property to `1536` **(1)** and Click on **Create** **(2)** under No vector search profiles.

      ![](../media/vector1.png)

27. On the **Vector profile** tab, Click on **Create** under No algorithm configurations.

      ![](../media/vector2.png)

28. On the **Vector algorithm** tab, leave the default and click on **Save**.

      ![](../media/vector3.png)

29. On the **Vector profile** tab, select the algorithm created in the previous step and Click on **Create** under No vectorizers.

      ![](../media/vector4.png)

30. On the **Vector algorithm** tab, leave the default and select the Azure OpenAI service as **Copilot-OpenAI-<inject key="Deployment ID" enableCopy="false"/>** and model deployment as **text-embedding-ada-002** . Click on **Save**.

      ![](../media/vector5.png)

31. On the **Vector profile** tab, select the Vectorizers created in the previous step and  Click on **Create** under No compression configurations.

      ![](../media/vector6.png)

32. On the **Compressions** tab, leave the default and click on **Save**.

      ![](../media/vector7.png)

33. In the **Vectore profile** tab, select Algorithm, Vectorizations, and Compressions recently created, and click on **Save**.

      ![](../media/vector8.png)

34. On the **Configure vector field** tab, keep the **Dimensions** property to `1536` and **Vector profile** created in previous step and Click on **Save**. Click on **Next: Create an indexer**.

    ![](../media/vector10.png)

35. Enter the **Indexer name** as **payroll-hr-cache**, and click on **Submit**.

      ![](../media/img89.png)

36. Navigate to the **Indexes** tab under the **Search management** section to view the newly created indexes, copy the index names, and save them in a text editor for later use.

      ![](../media/img90.png)

#### Validation

<validation step="4d8443a8-0de5-4a6c-ab23-621adb89ca44" />

### Task 3: Deploy the HR/Payroll Copilot application to Azure

In this task, you'll deploy the HR/Payroll Copilot application to Azure. You'll use a Bicep file to configure the necessary settings and then deploy the application using Azure Dev CLI commands.

1. In the LabVM, open File Explorer, navigate to the below-mentioned path, right-click on the `main.bicep` file, and select open with  **Visual Studio Code**.

      ```
      C:\LabFiles\OpenAIWorkshop\infra
      ```

    ![](../media/img41.png)

2. In the **appsettings** section of the `main.bicep` file, replace the values below with the ones you copied previously in the text editor. Next, press **CTRL + S** to save the file.

      ```
      AZURE_OPENAI_API_KEY:'YOUR_OPENAI_KEY' //#Replace it with the OpenAI key.
      AZURE_OPENAI_ENDPOINT:'YOUR_OPENAI_ENDPOINT' //#Replace it with the OpenAI Endpoint.
      AZURE_OPENAI_EMB_DEPLOYMENT:'YOUR_EMBEDDING_MODEL' //#Replace with your embedding model name.
      AZURE_OPENAI_CHAT_DEPLOYMENT:'YOUR_GPT_MODEL' //#Replace with your Open AI Chat Deployment name.
      AZURE_SEARCH_SERVICE_ENDPOINT:'YOUR_SEARCH_SERVICE_ENDPOINT' //#Replace with Search Service Endpoint.
      AZURE_SEARCH_ADMIN_KEY:'YOUR_SEARCH_SERVICE_KEY' //#Replace with your Search Service Admin Key.
      ```

     ![](../media/img42.png)

3. In the LabVM, navigate to Desktop and search for `cmd` in the search box, then click on **Command Prompt**.

     ![](../media/L2-T3-S3.png)

4. Run the below command to change the directory.

   ```bash
   cd C:\LabFiles\OpenAIWorkshop
   ```

5. Run the below command to **Authenticate with Azure**. It will redirect you to the Azure-authorized website. Next, select your account.

   ```bash
   azd auth login
   ```

6. Run the below command to set up the resource group deployment and **Create a new environment**. Make sure to replace `{DeploymentId}` with **<inject key="Deployment ID" enableCopy="true"/>** in the below command.

   ```bash
   azd config set alpha.resourceGroupDeployments on
   ```
   
   ```bash
   azd env new copilot-{DeploymentId}
   ```

7. Run the below command to provision Azure resources and deploy your project with a single command.

   ```bash
   azd up
   ```
   
8. Please select your Azure subscription to use, enter `1`, and click on the **Enter** button.

   ![](../media/img29.png)

9. Please select an Azure location to use, select the location as **<inject key="Region" enableCopy="false"/>** location, and click on the **Enter** button. You can change the location using the up and down arrows.

    ![](../media/img30.png)

10. Next, select **copilot-openai-<inject key="Deployment ID" enableCopy="False"/>** resource group and hit **ENTER**.

    ![](../media/img43.png)

11. Once the deployment succeeds, you will see the following message **SUCCESS: Your application was provisioned and deployed to Azure**. The deployment might take 5-10 minutes. It produces a web package file, then creates the resource and publishes the package for the app service.

    ![](../media/L2-T3-S11.png)

12. Navigate back to the Azure portal, search, and select **App service**. Select the available web app that you have deployed in the previous step.

    ![](../media/img44.png)

13. Next, click on **Browse** to open your Web application.

    ![](../media/img45.png)

    ![](../media/img46.png)

    > **Note**: If an issue occurs when you try to launch the app service, please restart the app service and wait five minutes before trying to launch the app again.

#### Validation

<validation step="de89d182-5c32-4a80-b44c-8fd6c706fdbe" />

## Summary

In this lab, you have accomplished the following:

- Built and configured the HR/Payroll Copilot application locally.
- Integrated Azure Cognitive Search to enhance search functionality within the application.
- Successfully deployed the application to Azure, making it accessible as a web service.

### You have successfully completed the lab
