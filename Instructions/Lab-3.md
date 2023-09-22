# Lab 3: Deploy and Run HR/Payroll Copilot Application 

   ![](../media/img13.png "Technical design")

**Application Platform:**
The solution is built on top of streamlit application platform. Streamlit allows the easy creation of interactive Python applications with the ability to render rich & responsive UI such as Chat UI and Python data visualization.

**Smart Agent: At the heart of the solution is the Python object Smart_Agent. The agent has the following components:**

  - **Goals/Tasks:** Smart_Agent is given a persona and instructions to follow to achieve certain goals, for example, HR Copilot is about helping answer HR/Payroll questions and update employee's personal information. This is done using instructions specified in the system message.

  - **NLP interaction & tool execution:** For the ability to use multiple tools and functions to accomplish business tasks, the function calling capability of the 0613 version is utilized to intelligently select the right function (validate identity/search knowledge base/update address/create ticket) based on the agent's judgment of what needs to be done. The agent is also able to engage with users following the instructions/goals defined in the system message.

  - **Memory:** The agent maintains a memory of the conversation history. The memory is backed by Streamlit's session state.
  - **LLM:** The agent is linked to a 0613 GPT-4 model to power its intelligence.

    
### Task 1: Build your own HR/Payroll copilot locally

1. In the LabVM, open File Explorer navigate to the `C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot` path, right-click on the `secrets.env` file and select open with  **Visual Studio Code**.

    ![](../media/img38.png)

1. The Visual Studio code is opened on the desktop. Edit the below code and update the **OpenAI Key**, **Embedding model and Chat gpt4 model**, **OpenAI Endpoint**, and **Cognitive search endpoint**, values which you have copied and stored in the text file earlier.

   ```
      AZURE_OPENAI_API_KEY:'YOUR_OPENAI_KEY' //#Replace with the OpenAI Key
      AZURE_OPENAI_ENDPOINT:'YOUR_OPENAI_ENDPOINT' //#Replace with the OpenAI Endpoint
      AZURE_OPENAI_EMB_DEPLOYMENT:'YOUR_EMBEDDING_MODEL' //#Replace with the name of your embedding model deployment
      AZURE_OPENAI_CHAT_DEPLOYMENT:'YOUR_GPT4_MODEL' //#Replace with the name of your Open AI Chat Deployment
      AZURE_SEARCH_SERVICE_ENDPOINT:'YOUR_SEARCH_SERVICE_ENDPOINT' //#Replace with Search Service Endpoint
   ```

1.  After updating values the `secrets.env` file should be as shown in the below screenshot, press **CTRL + S** to save the file.

    ![](../media/img39.png)

1. To run the application from the command line, navigate to Command Prompt and run the below command:

   >**Note**: Here, you can enter your email address below to get notifications. Otherwise, leave this field blank and click on **Enter**.

   ```
   cd C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot\employee_support
   streamlit run hr_copilot.py
   ```

1. Once the execution of `streamlit run hr_copilot.py` is completed. A locally hosted HR Copliot application will be opened in the web browser. 

   ![](../media/img17.png)
   ![](../media/img18.png)

1. Run the following query to validate the identity of the employee.

   ```
   John 1234
   ```

   ![](../media/img19.png)

1. Enter an example question such as `When will I receive W2 form?`. The questions are answered by the Copilot by searching a knowledge base and providing the answer.

   ![](../media/img23.png)

1. Copilot also can help update employee information like address updates. For other information update requests, Copilot will log a ticket to the HR team to update the information. Enter `I moved to 123 Main St, San Jose, CA 95112, please update my address` in the HR Copilot app.

    ![](../media/img24.png)

### Task 2: Deploy HR/Payroll copilot application to Azure

1. In the LabVM, open File Explorer navigate to the `C:\LabFiles\OpenAIWorkshop\infra` path, right-click on the `main.bicep` file, and select open with  **Visual Studio Code**.

    ![](../media/img41.png)

1. In the **appsettings** section of `main.bicep` file, replace the values below with the ones you copied previously in the text editor. Next, press **CTRL + S** to save the file.

      ```
      AZURE_OPENAI_API_KEY:'YOUR_OPENAI_KEY' //#Replace with the OpenAI Key
      AZURE_OPENAI_ENDPOINT:'YOUR_OPENAI_ENDPOINT' //#Replace with the OpenAI Endpoint
      AZURE_OPENAI_EMB_DEPLOYMENT:'YOUR_EMBEDDING_MODEL' //#Replace with the name of your embedding model deployment
      AZURE_OPENAI_CHAT_DEPLOYMENT:'YOUR_GPT4_MODEL' //#Replace with the name of your Open AI Chat Deployment
      AZURE_SEARCH_SERVICE_ENDPOINT:'YOUR_SEARCH_SERVICE_ENDPOINT' //#Replace with Search Service Endpoint
      ```

    ![](../media/img42.png)


1. In the LabVM, navigate to Desktop and search for `cmd` in the search box then click on **Command Prompt**.

1. Run the below command to change the directory.

   ```bash
   cd C:\LabFiles\OpenAIWorkshop
   ```

1. Run the below command to **Authenticate with Azure**. It will redirect to the Azure Authorize website, select your account.

   ```bash
   azd auth login
   ```

1. Run the below command to set up the resource group deployment and **Create a new environment**. Make sure to replace `{DeploymentId}` with **<inject key="Deployment ID" enableCopy="true"/>** in the below command.

   ```bash
   azd config set alpha.resourceGroupDeployments on
   ```
   
   ```bash
   azd env new copilot-{DeploymentId}
   ```

1. Run the below command to Provision Azure resources, and deploy your project with a single command.

   ```bash
   azd up
   ```
1. Please select your Azure Subscription to use, enter `1`, and click on the **Enter** button.

   ![](../media/img29.png)


1. Please select an Azure location to use, select the location as **<inject key="Region" enableCopy="false"/>** location, and click on the **Enter** button. You can change the location using the up and down arrow.

    ![](../media/img30.png)


1. Next, select **copilot-openai-<inject key="Deployment ID" enableCopy="False"/>** resource group and hit **ENTER**.

    ![](../media/img43.png)

1. Once the deployment succeeded, you will see the following message **SUCCESS: Your application was provisioned and deployed to Azure**. The deployment might take 5 - 10 minutes. It is producing a web package file, then creating the resource and publishing the package to the app service.


1. Navigate back to the Azure portal, search, and select **App service**. Select the available web app that you have deployed in the previous step.

    ![](../media/img44.png)

1. Next, click on **Browse** to open your Web application.

    ![](../media/img45.png)

    ![](../media/img46.png)
