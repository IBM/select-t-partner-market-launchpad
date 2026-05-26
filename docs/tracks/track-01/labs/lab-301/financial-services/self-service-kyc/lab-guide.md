# Lab guide for self service KYC agent

## Overview

Financial institutions must comply with Know Your Customer (KYC) regulations to verify customer identities and assess risk profiles. This lab demonstrates how to build an intelligent self-service KYC system using watsonx Orchestrate that automates document validation, PII extraction, and risk assessment. The solution combines agentic workflows for document processing with AI agents that perform Customer Due Diligence (CDD), Enhanced Due Diligence (EDD), and adverse news screening, while incorporating human-in-the-loop approvals for critical decisions.

## Pre-requisites

Make sure you've already setup the environment:

- [Lab Environment setup](../../../../lab-environment-setup.md)
- [ADK Installation](https://developer.watson-orchestrate.ibm.com/getting_started/installing){:target="_blank"}
- [Download](https://ibm.box.com/s/rib2j1hoj5k41isu1q7rneqk53j58zzu){:target="_blank"} the lab files

!!! example "Tavily API Key"

    To use the Tavily MCP server you need to create an API Key. **Sign-up for free researcher plan that is meant for creators which provides 1,000 API credits / month here**: [https://app.tavily.com/home](https://app.tavily.com/home){:target="_blank"}

## Reference Architecture

![image](../../../../../../assets/images/track01/financial-services/301/architecture.png)

## Key Components

- **self-service-kyc-agent** (Supervisor Agent) – Primary agent that orchestrates the KYC validation process, validates document completeness, accuracy and compliance.
- **cdd-agent** (Collaborator Agent) – Creates risk profiles based on customer type, country of residence, occupation and transaction type.
- **adverse-news-agent** (Collaborator Agent) – Evaluates risk based on KYC rules and analyzes for potentially exposed persons using web search.
- **edd-agent** (Collaborator Agent) – Triggered when CDD flags high risk. Gathers additional supporting data such as source of wealth and cross-border connections.
- **kyc_document_validation** (Agentic Workflow Tool) – Validates and extracts PII information from Aadhaar and PAN cards using document classification and extraction.
- **human_in_the_loop** (Agentic Workflow Tool) – Implements human approval checkpoints before invoking critical agents or tools.
- **Tavily Search** (MCP Server) – Provides web search capabilities to CDD, EDD, and adverse news agents for gathering external information.


## Steps

### Step 1: Build the KYC document processing agentic workflow

1. In watsonx Orchestrate, click on the hamburger menu and click on **Build**.
    ![flow-1](../../../../../../../assets/images/track01/financial-services/301/flows/1.png)

1. Click on **All tools**.
    ![flow-2](../../../../../../../assets/images/track01/financial-services/301/flows/2.png)

1. Select **Agentic workflow**.
    ![flow-3](../../../../../../../assets/images/track01/financial-services/301/flows/3.png)

1. Enter the Name as **kyc_document_validation** and click on **Start building**.
    ![flow-4](../../../../../../../assets/images/track01/financial-services/301/flows/4.png)

1. You will see the Agentic workflow canvas. Click on **Edit details**.
    ![flow-5](../../../../../../../assets/images/track01/financial-services/301/flows/5.png)

1. Enter the description as `Validate the document and extract PII information.` and click on **Done**.
    ![flow-5-1](../../../../../../../assets/images/track01/financial-services/301/flows/5-1.png)

1. Click on the **Add your first step +**. Select **Present to user** > **Message**.
    ![flow-6](../../../../../../../assets/images/track01/financial-services/301/flows/6.png)

1. Add the following message:
    ```
    Upload one of the following document:

    - **Front side** of PAN card                              
    - **Front side** of Aadhaar card                       
    ```
    ![flow-7](../../../../../../../assets/images/track01/financial-services/301/flows/7.png)

1. Click on the line below the node inside the green box and select **Collect from user** > **File upload**.
    ![flow-8](../../../../../../../assets/images/track01/financial-services/301/flows/8.png)

1. You can rename the node to **Upload Aadhaar or Pan card**.
    ![flow-9](../../../../../../../assets/images/track01/financial-services/301/flows/9.png)

1. Click on the arrow outside the green box and select **Add a flow activity** > **Document Classifier**.
    ![flow-10](../../../../../../../assets/images/track01/financial-services/301/flows/10.png)

1. Add two classes **aadhaar** and **pan_card** and hit enter.
    ![flow-11](../../../../../../../assets/images/track01/financial-services/301/flows/11.png)

1. Click on **Test classifier**, and upload the two documents from the downloaded folder. And you should see the classifier correctly classifying the documents. Click on **Done**.
    ![flow-12](../../../../../../../assets/images/track01/financial-services/301/flows/12.png)

1. Click on the arrow below the classifier, and select **Add a flow control** > **Branch**.
    ![flow-13](../../../../../../../assets/images/track01/financial-services/301/flows/13.png)

1. Click on the branch and rename it to **Aadhaar or Pan flows**.
    ![flow-17](../../../../../../../assets/images/track01/financial-services/301/flows/17.png)

1. Click on the **Edit condition** in path 1 and select the condition as `if class_name == pan_card`. And click on **:material-keyboard-backspace:** button.
    ![flow-18](../../../../../../../assets/images/track01/financial-services/301/flows/18.png)
> Note: `class_name` can be found under **Document classifier** node.

1. Rename the else flow to **Aadhaar flow** and click outside.
    ![flow-19](../../../../../../../assets/images/track01/financial-services/301/flows/19.png)

1. Click on **Add +** > **Add a flow activity** > **Document extractor**.
    ![flow-14](../../../../../../../assets/images/track01/financial-services/301/flows/14.png)

1. Select the **Unstructured**.
    ![flow-15](../../../../../../../assets/images/track01/financial-services/301/flows/15.png)

1. Edit the name to **Aadhaar extractor** and upload the document named `VM_aadhaar.pdf` from the downloaded directory.
    ![flow-16](../../../../../../../assets/images/track01/financial-services/301/flows/16.png)

1. Click on the models on top right and select the **llama-4-maverick-17b** model as we'll use that for the document extraction for our use case.
    ![flow-20](../../../../../../../assets/images/track01/financial-services/301/flows/20.png)

1. Click on **Add field** and add the following fields:
    - Name
    - DOB
    - City
    - IDnumber
    ![flow-22](../../../../../../../assets/images/track01/financial-services/301/flows/22.png)

1. You can see the multi-model will extract the PII from the PDF document. Close the window.
    ![flow-23](../../../../../../../assets/images/track01/financial-services/301/flows/23.png)

1. Under the else flow, Click on **Add +** > **Add a flow activity** > **Document extractor**.
    ![flow-24](../../../../../../../assets/images/track01/financial-services/301/flows/24.png)

1. Rename it to **Pan extractor**.
    ![flow-25](../../../../../../../assets/images/track01/financial-services/301/flows/25.png)

1. Click on **Add field** and add the following fields:
    - Name
    - DOB
    - IDnumber
    ![flow-26](../../../../../../../assets/images/track01/financial-services/301/flows/26.png)

1. Close the window and under the Aadhaar flow, click on the line and select **Present to user** > **Message**.
    ![flow-27](../../../../../../../assets/images/track01/financial-services/301/flows/27.png)

1. Add the following message:
    ```
    |ID|Name|DOB|City|
    |--|--|--|--|

    ```
    Select the variable icon and under **Aadhaar extractor**, add all the variables sepeared by `|` as shown.
    ![flow-28](../../../../../../../assets/images/track01/financial-services/301/flows/28.png)

1. All the variables are seperate by `|` so that the output is a markdown table format.
    ![flow-29](../../../../../../../assets/images/track01/financial-services/301/flows/29.png)

1. Similarly under Pan flow, click on the line and select **Present to user** > **Message**. And add the following message:
    ```
    |ID|Name|DOB|
    |--|--|--|

    ```
    Select the variable icon and under **Pan extractor**, add all the variables sepeared by `|` as shown.
    ![flow-30](../../../../../../../assets/images/track01/financial-services/301/flows/30.png)

1. Your flow should look something like this.
    ![flow-31](../../../../../../../assets/images/track01/financial-services/301/flows/31.png)

1. Click on the **Output** > **Add +**.
    ![flow-46](../../../../../../../assets/images/track01/financial-services/301/flows/46.png)

1. Add a **string** and name it as **class_name**.
    ![flow-47](../../../../../../../assets/images/track01/financial-services/301/flows/47.png)

1. Click on **Edit data mapping**.
    ![flow-48](../../../../../../../assets/images/track01/financial-services/301/flows/49.png)

1. You can see the class_name is auto mapped. You can leave it as it is or manually select the value.
    ![flow-49](../../../../../../../assets/images/track01/financial-services/301/flows/50.png)

1. To set manual variable, click on the **Variables** and select **class_name** under **Document classifier**.
    ![flow-50](../../../../../../../assets/images/track01/financial-services/301/flows/51.png)

1. Similarly add the following:
    - Name
    - DOB
    - City
    - IDnumber

    You can leave the data mapping to auto mapping.
    ![flow-51](../../../../../../../assets/images/track01/financial-services/301/flows/54.png)

1. Your flow should look something like this.
    ![flow-52](../../../../../../../assets/images/track01/financial-services/301/flows/53.png)

1. Click on **Done**.

### Step 2: Build Human in the loop agentic workflow

1. Similarly, create another agentic workflow tool, name it as **human_in_the_loop** and click on **start building**.
    ![flow-32](../../../../../../../assets/images/track01/financial-services/301/flows/32.png)

1. Click on **edit details** and enter the description as **Adding human in the loop to get feedback on next steps**.
    ![flow-33](../../../../../../../assets/images/track01/financial-services/301/flows/33.png)

1. Click on **Parameters** and under input click on **Add input +** and add a **string** input.
    ![flow-34](../../../../../../../assets/images/track01/financial-services/301/flows/34.png)

1. Name: `agent_or_tool_name`, description: `Agent or tool name to get permission before invoke` and click **add**.
    ![flow-35](../../../../../../../assets/images/track01/financial-services/301/flows/35.png)

1. You will have two input variables now that the agent will make use to invoke this workflow. Click on **Done** to close the window.
    ![flow-36](../../../../../../../assets/images/track01/financial-services/301/flows/36.png)

1. Add the field **Date of Birth** and click on **Done**.
    ![flow-37](../../../../../../../assets/images/track01/financial-services/301/flows/37.png)

1. Click on the **Add your first step +**. Select **Present to user** > **Message**.
    ![flow-38](../../../../../../../assets/images/track01/financial-services/301/flows/38.png)

1. Add the following message:
    ```
    {flow.input.reasoning_why}. I want to invoke the **{flow.input.agent_or_tool_name}**.                     
    ```
    You will see the variables added automatically.
    ![flow-39](../../../../../../../assets/images/track01/financial-services/301/flows/39.png)

1. Click on the line below the node inside the green box and select **Collect from user** > **Boolean choice**. Rename it to **Do you authorize?**.
    ![flow-40](../../../../../../../assets/images/track01/financial-services/301/flows/40.png)

1. Click on done to save the workflow.
    ![flow-41](../../../../../../../assets/images/track01/financial-services/301/flows/41.png)

1. You should now have both the workflow tools completed.
    ![flow-42](../../../../../../../assets/images/track01/financial-services/301/flows/42.png)

### Step 3: Develop the AI Agents with AI-assisted coding

1. Download and open the self-service-kyc-assistant directory in IBM Bob IDE.
2. Once opened, sign in to Bob.
3. Now start prompting Bob to start building.
4. Type:
    ```
    @/agents Create the agents. I'll describe what each agent are suppose to do
    ```
    ![bob-1](../../../../../../assets/images/track01/financial-services/301/1.png)
5. Bob will ask for the details of each agent, and the intended workflow. Type the following prompt and hit enter:
    ```
    self-service-kyc-agent: Agent that validates the completeness, accuracy and compliance of documents.
    cdd-agent: Create a risk profile for the customer based on customer type, country of residence, occupation & transaction type. Example input: Create a risk profile for Vijay Mallya, Bengaluru, 18/12/1955.
    adverse-news-agent: Evaluate Risk based on KYC rules and also analyze for potentially exposed persons.
    edd-agent: Triggered only if Customer Due Diligence agent flags high risk. Gather more supporting data such as source of wealth, cross border connection and more. example input: Create a edd risk profile for Vijay Mallya, Bengaluru, 18/12/1955.

    The self-service-kyc-agent is the primary supervisor agent that collaborates with adverse-news-agent, cdd-agent, and edd-agent.

    The specific worlfow is as follows:

    Step 1: Use kyc_document_validation tool directly (no approval needed) to extract customer details from uploaded documents.
    Step 2: Before invoking adverse_news_agent, use human_in_the_loop tool for approval. If it returns false, stop execution and politely inform the user. If approved, delegate to adverse_news_agent to get adverse risk profile.
    Step 3: Before invoking cdd_agent, use human_in_the_loop tool for approval. If it returns false, stop execution and politely inform the user. If approved, delegate to cdd_agent to create CDD risk profile.
    Step 4: If CDD indicates HIGH RISK, use human_in_the_loop tool for approval before invoking edd_agent. If approved, delegate to edd_agent for extended due diligence.
    Step 5: Present results in this exact format:
    - Customer Details table (name, aadhar/dl/pan number, date of birth)
    - Adverse News table
    - CDD Risk Profile table
    - EDD Risk Profile table (if applicable)
    - Conclusion (2-3 sentences summarizing overall risk)
    Step 6: End with: "> AI generated response: AI can make mistakes, use with caution."
    ```
    ![bob-2](../../../../../../assets/images/track01/financial-services/301/2.png)
6. A todo list will be created, verify it and approve the execution.
7. Bob should refer to the `best_practices.md` and write the instructions in the agent.yaml. If it skips reading the file you can explictly prompt to refer the best_practices.md and write the instructions. Once done, you will see the agent.yaml updated with the right collaborators, tools, description and instructions. Go ahead and **Approve it**.
    ![bob-3](../../../../../../assets/images/track01/financial-services/301/3.png)
8. We will add **Tavily** MCP server to the cdd, edd and adverse-news agent so that these agents get access to the internet. Change the Bob mode to **Advanced** and type the following prompt and hit enter:
    ```
    I want to use the Tavily search MCP server for the cdd, edd and adverse news agent, can you refer the watsonx orchestrate documentation and add the Tavily search MCP server with the search tool?
    ```
    ![bob-4](../../../../../../assets/images/track01/financial-services/301/4.png)
9. You will see that, bob now tries to connect to the watsonx Orchestrate documentation MCP server to find information regarding tavily search. **Approve** it.
    ![bob-5](../../../../../../assets/images/track01/financial-services/301/5.png)
10. Bob may try to read multiple documents, **Approve** them all.
11. You will see the tool getting added to the agent.
    ![bob-6](../../../../../../assets/images/track01/financial-services/301/6.png)
12. Similarly **Approve** the edd-agent and adverse-news agent.
    ![bob-7](../../../../../../assets/images/track01/financial-services/301/7.png)
13. The agent configuration is now ready! we can deploy it on watsonx Orchestrate. Click on **Start New Task**.
    ![bob-8](../../../../../../assets/images/track01/financial-services/301/8.png)

### Step 4: Activate the watsonx Orchestrate environment through the ADK

1. In terminal run the following command to activate your orchestrate environment:
    ```
    orchestrate env activate pm-launchpad --api-key <YOUR-API-KEY>
    ```
> You have learn't how to get an env and activate it in the [Lab Environment setup](../../../../lab-environment-setup.md)

### Step 5: Deploy the agent and MCP server on watsonx Orchestrate environment through Bob

1. Type the prompt:
    ```
    I'm connected to my watsonx orchestrate instance, I need you to do the following:
    1. Create a connection for tavily, and add the tavily api key
    2. Import the agents and tools
    3. Deploy the self-service-kyc-assistant

    Documentation to refer @/connections_best_practices.md , @/toolkit_best_practices.md 
    ```

    ![bob-deploy-1](../../../../../../assets/images/track01/financial-services/301/9.png)

1. Review the tasks and **approve** it.
    ![bob-deploy-2](../../../../../../assets/images/track01/financial-services/301/10.png)

1. Bob will first create the connection, configure it for both draft and live environment **approve** it.
    ![bob-deploy-3](../../../../../../assets/images/track01/financial-services/301/11.png)

1. Bob will ask you how would you like to set the Tavily API key. You can pass it to Bob via prompt, or set manually. As a best practice you can set the credentials manually. Type:
    ```
    Give me the command, I'll set it manually
    ```
    ![bob-deploy-4](../../../../../../assets/images/track01/financial-services/301/12.png)

1. Run the two commands in terminal with your tavily api key.
    ![bob-deploy-5](../../../../../../assets/images/track01/financial-services/301/13.png)
> Note: Bob may make mistake with this command instead of `-e` it may give `--env` and you may get the following error : 
> 
> Invalid value for '--environment' / '--env': 'TAVILY_API_KEY=<<your-api-key>>' is not one of 'draft', 'live'.
>
> In that case simply use these correct commands: 
> 
> `orchestrate connections set-credentials --app-id tavily --env draft -e TAVILY_API_KEY=<your_tavily_api_key>`
>
> `orchestrate connections set-credentials --app-id tavily --env live -e TAVILY_API_KEY=<your_tavily_api_key>`

1. Upon approval, you will see Bob will try to import the Tavily MCP server. Click on **Run**.
    ![bob-deploy-6](../../../../../../assets/images/track01/financial-services/301/14.png)

1. Finally, Bob will try to import all the agents, it may fail by importing the agents in wrong order, however it will correct itself. If not, you can give the prompt:
    ```
    First the collaborator agents need to be deployed then the self-service
    ```

    ![bob-deploy-7](../../../../../../assets/images/track01/financial-services/301/15.png)

1. The tool names may also be different in the wxO instance and the agent.yaml, in that case Bob will list the tools and get the correct name and replace it in the YAML.
    ![bob-deploy-8](../../../../../../assets/images/track01/financial-services/301/16.png)
    ![bob-deploy-18](../../../../../../assets/images/track01/financial-services/301/18.png)

1. The adverse news, cdd and edd agents will be deployed first and then the self-service KYC agent.
    ![bob-deploy-9](../../../../../../assets/images/track01/financial-services/301/17.png)

1. You will get a summary at the end once all the steps are completed.
    ![bob-deploy-19](../../../../../../assets/images/track01/financial-services/301/19.png)

### Step 6: Verify and test the agent

1. Login to [cloud.ibm.com](cloud.ibm.com) > **resources** > **AI/ML** > **orchestrate** > **Launch Instance**.
1. Go to **Manage agents** and select the **self_service_kyc_agent**.
1. Verify the workflow tools added.
    ![wxo-1](../../../../../../assets/images/track01/financial-services/301/20.png)
1. You can also see the adverse news, cdd and edd agent as collaborator agents.
    ![wxo-2](../../../../../../assets/images/track01/financial-services/301/21.png)
1. You can also see the Behavior added to the agent as per the [Best practices](https://developer.watson-orchestrate.ibm.com/agents/descriptions#best-practices-for-writing-instructions) specified by the wxO documentation.
    ![wxo-3](../../../../../../assets/images/track01/financial-services/301/22.png)
1. Click on **Validate KYC Document** in the chat widget on the right and you will see the workflow getting invoked, prompting to upload a file.
    ![wxo-4](../../../../../../assets/images/track01/financial-services/301/23.png)
1. Click on **Validate KYC Document** in the chat widget on the right and you will see the workflow getting invoked, prompting to upload a file.
    ![wxo-5](../../../../../../assets/images/track01/financial-services/301/23.png)
1. Go ahead and upload any Aadhaar or Pan card or use the ones provided as part of the lab. Once uploaded, the agent will ask you to review the document. This is Human-in-the-loop(HITL) capability of watsonx Orchestrate. Click on **view**.
    ![wxo-6](../../../../../../assets/images/track01/financial-services/301/24.png)
1. Review the fields and click on **submit**.
    ![wxo-7](../../../../../../assets/images/track01/financial-services/301/25.png)
1. The workflow will extract the PII information and present in the table. Furthermore, the HITL will ask confirmation at each step when the agent requires collaboration with another agent or tool. Click on **Yes** when prompted.
    ![wxo-8](../../../../../../assets/images/track01/financial-services/301/26.png)
    ![wxo-9](../../../../../../assets/images/track01/financial-services/301/27.png)
    ![wxo-10](../../../../../../assets/images/track01/financial-services/301/28.png)
1. The final response will contain the risk profiles of the person along with the PII details and a conclusion section.
    ![wxo-11](../../../../../../assets/images/track01/financial-services/301/29.png)
    ![wxo-12](../../../../../../assets/images/track01/financial-services/301/30.png)
    ![wxo-13](../../../../../../assets/images/track01/financial-services/301/31.png)

!!! success "Conclusion"

    👏 Congratulations on completing the lab! 🎉