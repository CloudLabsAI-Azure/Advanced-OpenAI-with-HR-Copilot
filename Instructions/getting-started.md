# Build your own Intelligent HR Copilot with Azure Open AI

### Overall Estimated Duration: 4 Hours

## Overview

In this hands-on-lab, you will set up the Azure OpenAI resource and install the application locally. Over the past few years, language models like GPT-3 and GPT-4 have proven their versatility across various applications. The latest Azure OpenAI Service now includes a feature called function calling, which allows GPT-3 and GPT-4 to generate structured JSON outputs based on predefined functions. This integration capability enables developers to connect these models with other systems and tools, enhancing their functionality. In this overview, we will explore how function calling operates, examine its use cases, and guide you through leveraging this feature within the Azure OpenAI Service. Additionally, we'll introduce the Smart_Agent Python object, detailing its components like goals/tasks, NLP interaction and tool execution, memory management, and its integration with a multi-agent copilot model. This model utilizes specialist agents managed by an agent runner, ensuring efficient task handling and continuity across different domains.

## Objective

By the end of this lab, you will be able to:

- **Getting Started with Building a Chat Application**:
- **Understand function calling in Open AI GPT**:
- **Deploy and Run the HR/Payroll Copilot Application**:
- **Understand HR Copilot Demo Application**:
  
## Pre-requisites

1. **Familiarity with GPT Models**: Familiarity with GPT-3 and GPT-4, including their capabilities and use cases.
2. **Experience with REST APIs**: Familiarity with REST APIs, as function calling involves interacting with APIs.
3. **Basic Programming Skills**: Proficiency in Python programming to follow along with the Smart_Agent Python object setup and multi-agent copilot model implementation.

## Architecture



## Architecture Diagram

 ![Access Your VM and Lab Guide](../media/arch20.png)

## Explanation of Components

## Getting Started with the Lab

1. After the environment has been set up, your browser will load a virtual machine (JumpVM) and the lab manual. Use this virtual machine throughout the workshop to perform the lab. You can see the number on the bottom of the lab guide to switch to different exercises in the lab guide.

   ![](../media/getstartpage-01a.png)
 
1. To get the lab environment details, you can select the **Environment Details** tab. Additionally, the credentials will also be emailed to your registered email address. Additionally, under the **Resources** tab, you may start, stop, and restart virtual machines.

   ![](../media/getstartpage-02a.png "Enter Email")
 
   > You will see the SUFFIX value on the **Environment Details** tab; use it wherever you see SUFFIX or DeploymentID in lab steps.
 
## Login to the Azure Portal

1. In the JumpVM, click on the Azure portal shortcut of the Microsoft Edge browser, which is created on the desktop.

   ![](../media/open-azureportal.png "Enter Email")
   
2. On the **Sign in to Microsoft Azure** tab, you will see the login screen. Enter the following email or username, and click on **Next**. 

   * **Email/Username**: <inject key="AzureAdUserEmail"></inject>
   
      ![](../media/signin-uname.png "Enter Email")
     
3. Now enter the following password and click on **Sign in**.
   
   * **Password**: <inject key="AzureAdUserPassword"></inject>
   
      ![](../media/signin-pword.png "Enter Password")
     
4. If you see the pop-up **Stay Signed in?**, select **No**.

5. If you see the pop-up **You have free Azure Advisor recommendations!**, close the window to continue the lab.

6. If a **Welcome to Microsoft Azure** popup window appears, select **Maybe Later** to skip the tour.
   
7. Now that you will see the Azure Portal Dashboard, click on **Resource groups** from the Navigate panel to see the resource groups.

   ![](../media/select-rg.png "Resource groups")

8. Click "Next" from the bottom right corner to embark on your Lab journey!

     ![](../media/next.png)
