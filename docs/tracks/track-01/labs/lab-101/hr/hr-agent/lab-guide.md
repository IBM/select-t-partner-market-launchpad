# AskHR: Automate HR tasks with Agentic AI

## Pre-requisites

- Make sure you've already setup the environment:
- [Lab Environment setup](../../../../lab-environment-setup.md)
- [ADK Installation](https://developer.watson-orchestrate.ibm.com/getting_started/installing){:target="_blank"}
- [Download files](https://ibm.box.com/s/n0pkqfjzwxi3cvzaq8msaclfnf7mbwro){:target="_blank"} 
- Download the zip file from Lab1 folder <br>
Note: If you are an instructor, complete the instructor guide and update the url in hr.yaml. If you are a practitioner, obtain the updated hr.yaml file from your instructor. Do not directly use the yaml file to import into Orchestrate. 
- If you are an instructor, complete the [instructor set-up guide](https://github.ibm.com/skol/agentic-ai-client-bootcamp-instructors/blob/main/usecase-setup/askhr/DEPLOY_MANUAL.md) and update the hr.yaml with new url after completing the setup. 

## Step by step instructions to build the HR Agent

1. When you launch watsonx Orchestrate, you'll be directed to this page. Click on the hamburger menu in the top left corner:

    ![img.png](../../../../../../assets/images/track01/hr/101/step1.png)

2. Click on the down arrow next to **Build**. Then click on **Agent Builder**:

    ![img.png](../../../../../../assets/images/track01/hr/101/step2.png)

3. Click on **Create agent +**:

    ![img.png](../../../../../../assets/images/track01/hr/101/step3.png)

4. Select "Create from scratch", give your agent a name, e.g. "HR Agent", and fill in the description as shown below:

    ```
    You are an agent who handles employee HR queries.  You provide short and crisp responses, keeping the output to 200 words or less.  You can help users check their profile data, retrieve latest time off balance, update title or address, and request time off. You can also answer general questions about company benefits.
    ```  

5. Click on **Create**

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step4.png)

6. Scroll down the screen to the **Knowledge** section. Copy the following description into the **Knowledge Description** section:

    ```
    This knowledge base addresses the company's employee benefits, including parental leaves, pet policy, flexible work arrangements, and student loan repayment.
    ```

7. Click on **Upload files**

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step5.png)

8. Upload the **Employee Benefits.pdf** and click on **Upload**:

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step6.png)  

9. Wait until the file has been uploaded successfully and double check that it is now shown in the Knowledge section:

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step7.png)  

10. Scroll down to the **Toolset** section. Click on **Add tool +**:

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step8.png)

11. Select **Import**

    <!-- ![img.png](../../../../../../assets/images/track01/hr/101/step13.png) -->

12. Drag and drop or click to upload the **hr.yaml** file (provided to you by the instructor), then click on **Next**: <br>
Note: Instructors make sure the url in the hr.yaml is updated after [instructor set up](https://github.ibm.com/skol/agentic-ai-client-bootcamp-instructors/tree/main/usecase-setup/askhr) before providing to clients. 

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step10.png)

13. Select all the operations and click on **Done**:

    ![img.png](../../../../../../assets/images/track01/hr/101/step-import.jpg)

14. Scroll down to the **Behavior** section. Insert the instructions below into the **Instructions** field:

    ```
    Use your knowledge base to answer general questions about employee benefits. 

    Use the tools to get or update user specific information.

    When user asks to show profile data or check time off balance or update title/address or request time off for the very first time,  first ask the user for their name,  then invoke the tool and then use the same name in the whole session without asking for the name again.

    When the user requests time off, convert the dates to YYYY-MM-DD format, e.g. 5/22/2025 should be converted to 2025-05-22 before passing the date to the post_request_time_off tool.
    ```

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step12.png)

13. Test your agent in the preview chat on the right side by asking the following questions and validating the responses.  They should look similar to what is shown in the screenshots below:

    ```
    1. What is the pet policy? 

    2. Show me my profile data.

    3. I'd like to update my title. 

    4. Update my address

    5. What is my time off balance?

    6. Request time off

    7. Show my profile data.

    ```

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step13.png)

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step13_2.png)

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step13_3.png)

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step13_4.png)

14. Once you have validated the answers, click on **Deploy** in the top right corner to deploy your agent:

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step14.png)

15. Click on the hamburger menu in the top left corner and then click on **Chat**:

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step15.png)

16. Make sure **HR Agent** is selected. You can now test your agent:

    ![img.png](../../../../../../assets/images/track01/hr/101/hr_step16.png)

!!! success "Conclusion"

    👏 Congratulations on completing the lab! 🎉
