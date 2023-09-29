# Lab 2: Understand function calling in Open AI GPT

Over the last couple of years, language models like GPT-3 and GPT-4 have demonstrated their immense power and versatility. These models have been successfully applied in various scenarios, showcasing their capabilities. While these models are already valuable on their own, Azure OpenAI Service now offers an exciting new feature called function calling. With function calling, the latest versions of GPT-3 and GPT-4 can generate structured JSON outputs based on functions specified in the request. This allows developers to integrate the models with other systems and tools, enabling even more possibilities. It's important to note that while the models can generate the function calls, the execution of these calls remains under your control, ensuring that you maintain full control over the process. In this overview, we will explore how function calling works, provide examples of its use cases, and guide you through the steps to leverage this powerful feature in Azure OpenAI Service. 

To know more about Azure Function calling please refer to [Function calling is now available in Azure OpenAI Service](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/function-calling-is-now-available-in-azure-openai-service/ba-p/3879241).


### Task 1: Understand Function calling 

1. Open **Visual Studio Code** from the desktop, next click on **File** and select **Open Folder**.

    ![](../media/img55.png) 

1. Navigate to `C:\LabFiles\openai\Basic_Samples\Functions` and click on **Select folder**. 

    ![](../media/img56.png) 

1.  On the **Do you trust the authors of the files in this folder?** pop-up check the box next to **Trust the authors of all files in the parent folder 'Basic_Samples'**, and select **Yes, I trust the authors**.

    ![](../media/img57.png) 

1. In the **Functions** folder open `config.json` and replace the values following values with the ones you copied earlier.

    **DEPLOYMENT_ID**: `Replace the value with gpt-model name`
    **OPENAI_API_BASE**: `Replace the value with OpenAI Endpoint`
    **SEARCH_SERVICE_ENDPOINT**: `Replace the value with Search Service Endpoint`

    ![](../media/img58.png) 

