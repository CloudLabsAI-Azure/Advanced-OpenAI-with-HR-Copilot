# Lab 2: Understand function calling in Open AI GPT

Over the last couple of years, language models like GPT-3 and GPT-4 have demonstrated their immense power and versatility. These models have been successfully applied in various scenarios, showcasing their capabilities. While these models are already valuable on their own, Azure OpenAI Service now offers an exciting new feature called function calling. With function calling, the latest versions of GPT-3 and GPT-4 can generate structured JSON outputs based on functions specified in the request. This allows developers to integrate the models with other systems and tools, enabling even more possibilities. It's important to note that while the models can generate the function calls, the execution of these calls remains under your control, ensuring that you maintain full control over the process. In this overview, we will explore how function calling works, provide examples of its use cases, and guide you through the steps to leverage this powerful feature in Azure OpenAI Service. 

To know more about Azure Function calling please refer [Function calling is now available in Azure OpenAI Service](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/function-calling-is-now-available-in-azure-openai-service/ba-p/3879241).

## Exercise 1: Deploy and Run HR/Payroll Copilot Application 

   ![](../media/img13.png "Technical design")

**Application Platform:**
The solution is built on top of streamlit application platform. Streamlit allows easy creation of interactive Python application with ability to render rich & responsive UI such as Chat UI and Python data visualization.

**Smart Agent:At the heart of the solution is the python object Smart_Agent. The agent has following components:**

  - **Goals/Tasks:** Smart_Agent is given a persona and instructions to follow to achieve certain goals, for example for HR Copilot it is about helping answer HR/Payroll question and update employee's personal information. This is done using instructions specified to the system message.

  - **NLP interacation & tool execution:** For the abilility to use multiple tools and functions to accomplish business tasks, function calling capability of 0613 version is utilized to intelligently select the right function (validate identity/search knowlege base/update address/create ticket) based on the agent's judgement of what need to be done. The agent is also able to engage with users following the instruction/goals defined in the system message.

  - **Memory:** The agent maintain a memomory of the conversation history. The memory is backed by Streamlit's session state.
  - **LLM:** The agent is linked to a 0613 GPT-4 model to power its intelligence.

### Task 1: Understand Function calling (Read-Only)

1. In the LabVM, open File Explorer naviagte to the `C:\Labfiles\OpenAIWorkshop\scenarios\incubations\copilot\employee_support` path, open hr_copilot_utils.py, and select Open with  **Visual Studio Code** click on **OK**. Take a look at the code to see function calling works.

    ![](../media/img25.png)

2. The code snippet here provides a persona description for an **HR support specialist** named Lucy. Lucy's role is to assist employees with HR and Payroll-related questions and handle personal information updates. 

    ![](../media/img26.png)
   
3. In the code snippet, you can see how the different function specifications are defined, each specification will help find relevant answers to HR and Payroll questions.

    ![](../media/img27.png)

4. Once the application runs you will observe how the function is called and details are fetched.

    ![](../media/img28.png)

### Task 2: Build your own HR/Payroll copilot locally

1. In the LabVM, navigate to Desktop and search for `cmd` in the search box then click on **Command Prompt**.

2. Run the below command to change the directory.

   ```
   cd C:\LabFiles\OpenAIWorkshop-Automation\scenarios\incubations\copilot
   ```

3. Provide settings for Open AI and Database by creating a ```secrets.env``` file in the root of this folder by running the below command.

   ```
   code secrets.env
   ```
4. You will see the Visual Studio code is opened in the desktop. Enter the below code and update the OpenAI Key, Model Name and Endpoint values which you have copied and stored in text file earlier.

   ```
   AZURE_OPENAI_API_KEY="********************************" #Replace with the OpenAI Key
   AZURE_OPENAI_GPT4_DEPLOYMENT="NAME_OF_GPT_4_DEPLOYMENT" #Replace with the OpenAI Model Name
   AZURE_OPENAI_ENDPOINT=https://openairesourcename.openai.azure.com/ #Replace with the OpenAI Endpoint
   USE_AZCS="False"
   AZURE_OPENAI_API_VERSION="2023-05-01"
   USE_SEMANTIC_CACHE="False"
   SEMANTIC_HIT_THRESHOLD=0.9
   ```

5.  After updating values the `secrets.env` file should be as shown in the below screenshot, press **CTRL + S** to save the file.

    ![](../media/img16.png)

6. To run the application from the command line navigate back to Command Prompt and run the below command:

   >**Note**: Here, you can enter your email address below to get notifications. Otherwise, leave this field blank and click on **Enter**.

   ```
   cd employee_support
   streamlit run hr_copilot.py
   ```

7. Once the execution of `streamlit run app.py` is completed. A locally hosted HR Copliot appliation will be opened in the web browser. 

   ![](../media/img17.png)
   ![](../media/img18.png)

8. Run the following query to validate the identity of the employee.

   ```
   Jhon 1234
   ```

   ![](../media/img19.png)

9. Enter an example question such as `When will I receive W2 form?`. The questions are answered by the Copilot by searching a knowledge base and providing the answer.

   ![](../media/img23.png)

10. Copilot also can help update employee information like address update. For other information update requests, the Copilot will log a ticket to the HR team to update the information. Enter 'I moved to 123 Main St, San Jose, CA 95112, please update my address' in the HR Copilot app.

    ![](../media/img24.png)
