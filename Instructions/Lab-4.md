# Lab 4: Understand HR Copilot demo Application 

When scope for automation spans across multiple functional domains, like human, agent may perform better when it can specialize in a single area. So instead of stuffing a single agent with multiple capabilities, we can employ multiple agents model, each specializing in a single domain. These agents are managed and coordinated by a manager agent (agent runner). This is called multi-agent copilot model. The agent runner is responsible to promote the right agent from the agent pool to be the active agent to interact with user. It also is responsible to transfer relavant contextfrom agent to agent to ensure continuity. In this model, the agent runner relies on the specialist agent's cue to back-off from conversation to start the transfer. Each specialist agent has to implement a skill to send a notification (back-off method) when it thinks its skillset cannot handle the user's request. On the other hand, the decision on exactly which agent should be selected to take over the conversation is still with agent runner. When receiving such request, agent runner will revaluate the from the input by the requesting agent to decide on which agent to select for the job. This skill also relies on a LLM. Agent runner runs each specialist agent's run method. There can be some persistent context that should be available across agent's sessions. This is implemented as the persistent memory at agent runner. Each specialist agent depending on the requirement for skill, can be powered by a gpt-35-turbo or gpt-4. Multi-agent solution has same application platform (streamlit) as the single HR Copilot.

![](../media/img20.png)


## Exercise 1: Deploy and Run Multi-agent Copilot Application

### Task 1:  Build your own Multi-agent Copilot application locally

1. In the LabVM, navigate to Desktop and search for `cmd` in the search box then click on **Command Prompt**.

2. Run the below command to change the directory.

   ```
   cd C:\LabFiles\OpenAIWorkshop\scenarios\incubations\copilot\employee_support
   ```

3. To run the application from the command line navigate back to Command Prompt and run the below command:

   >**Note**: Here, you can enter your email address below to get notifications. Otherwise, leave this field blank and click on **Enter**.

   ```
   streamlit run multi_agent_copilot.py
   ```

4. Once the execution of `streamlit run multi_agent_copilot.py` is completed. A locally hosted HR Copliot appliation will be opened in the web browser. 

   ![](../media/img21.png)

   ![](../media/img22.png)

5. Run the following query to validate the identity of the employee.

   ```
   Sharon 1234
   ```

   ![](../media/img47.png)

6. Enter an example question such as `how to do I reset my password?`. The questions are answered by the Copilot by searching a knowledge base and providing the answer.

   ![](../media/img48.png)

### Task 2: Deploy Multi-agent copilot application to Azure

1. In the LabVM, open File Explorer naviagte to the `C:\LabFiles\OpenAIWorkshop\infra` path, right click on `main.bicep` file and select open with  **Visual Studio Code**.

    ![](../media/img41.png)

1. In the `main.bicep` file, replace the file name in **Line 49** to `multi_agent_copilot.py` and press **CTRL + S** to save the file.

    ![](../media/img51.png)

1. In the LabVM, navigate to Desktop and search for `cmd` in the search box then click on **Command Prompt**.

1. Run the below command to change the directory.

   ```bash
   cd C:\LabFiles\OpenAIWorkshop
   ```

1. Run the below command to **Authenticate with Azure**. It will redirect to Azure authorize website, select your account.

   ```bash
   azd auth login
   ```

1. Run the below command to setup the resource group deployment and **Create a new environment**. Make sure to replace `{DeploymentId}` with **<inject key="Deployment ID" enableCopy="true"/>** in the below command.

   ```bash
   azd config set alpha.resourceGroupDeployments on
   ```
   
   ```bash
   azd env new azure-copilot-{DeploymentId}
   ```

1. Run the below command to Provision Azure resources, and deploy your project with a single command.

   ```bash
   azd up
   ```
1. Please select your Azure Subscription to use, enter `1` and click on **Enter** button.

   ![](../media/img29.png)


1. Please select an Azure location to use, select the location as **<inject key="Region" enableCopy="false"/>** location, and click on **Enter** button. You can change the location using up and down arrow.

    ![](../media/img30.png)


1.  Next, select **multiagent-<inject key="Deployment ID" enableCopy="False"/>** resource group and hit **ENTER**.

    ![](../media/img50.png)

1. Once the deployment succeeded, you will see the following message **SUCCESS: Your application was provisioned and deployed to Azure**. The deployment might take 5 - 10 minutes. It is producing a web package file, then creating the resource and publishing the package to the app service.


1. Naviagte back to the Azure portal, select **App service** from **multiagent-<inject key="Deployment ID" enableCopy="False"/>** resource group .

    ![](../media/img52.png)

1. Next, click on **Browse** to open your Web application.

    ![](../media/img53.png)

    ![](../media/img46.png)

   > **Note**: If an issue occurs when you try to launch the app service, please restart the app service and wait five minutes before trying to launch the app again.
