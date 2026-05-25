# Lab guide for IT Service Manager

## Overview

In this lab, you will configure and deploy a pre-built IT Service Manager agent that integrates with ServiceNow to handle incident management, ticket creation, task assignment, and knowledge base access. This agent enables employees to interact with IT services through natural language, streamlining support operations and improving response times.

## Pre-requisites

- Make sure you've already setup the environment:
- [Lab Environment setup](../../../../lab-environment-setup.md)
- Access to watsonx Orchestrate
- ServiceNow instance with ITSM module enabled
- ServiceNow credentials with appropriate permissions
- Basic understanding of ITSM concepts

## Reference Architecture

The IT Service Manager follows an integrated architecture:

1. **User Interface Layer:** Chat interface where employees submit IT requests and check ticket status
2. **Agent Layer:** watsonx Orchestrate agent that processes requests and orchestrates ServiceNow operations
3. **Integration Layer:** ServiceNow REST API connections for ITSM operations
4. **ServiceNow Platform:** Backend ITSM system managing incidents, tasks, and knowledge base

**Key Components:**

- **IT Service Manager Agent:** Pre-built agent from watsonx Orchestrate catalog
- **ServiceNow Connector:** Authenticated connection to ServiceNow instance
- **Incident Management Tools:** Create, update, retrieve, and close incidents
- **Task Assignment Engine:** Automatically routes and assigns tasks to IT teams
- **Knowledge Base Integration:** Access to ServiceNow knowledge articles
- **Asset Management Tools:** Track and manage IT assets and equipment

## Steps

### 1. Access the Pre-built Agent

1. Open the watsonx Orchestrate UI
2. Navigate to the **Catalog** section
3. Search for "ServiceNow" or "IT Service Manager"
4. Click on the **IT Service Manager** agent card
5. Click **Use this agent** to add it to your workspace

### 2. Configure ServiceNow Connection

Before using the agent, you need to establish a connection to your ServiceNow instance.

#### 2.1 Create ServiceNow Connection

1. Navigate to **Connections** in the left sidebar
2. Click **Add connection**
3. Search for "ServiceNow" and select it
4. Enter your ServiceNow connection details:
   - **Instance URL:** Your ServiceNow instance URL (e.g., `https://your-instance.service-now.com`)
   - **Username:** ServiceNow user with ITSM permissions
   - **Password:** ServiceNow user password
   - **Connection Name:** "ServiceNow ITSM"

5. Click **Test connection** to verify connectivity
6. Click **Save** once the test is successful

#### 2.2 Link Connection to Agent

1. Open the **IT Service Manager** agent in Agent Builder
2. Navigate to the **Toolset** section
3. For each ServiceNow tool, click the settings icon
4. Select the ServiceNow connection you created
5. Click **Save**

### 3. Configure Agent Profile

1. In the **Profile** section, review and customize:
   - **Purpose:** "Assist employees with IT service requests, incident management, and knowledge base access"
   - **Usage Scenarios:** "Use this agent for creating incidents, checking ticket status, accessing IT knowledge, and managing IT assets"
   - **Interaction Style:** Keep as **Default** for natural conversation flow

### 4. Review Available Tools

The pre-built agent includes the following tools:

#### 4.1 Incident Management Tools

- **create_incident:** Create new IT incidents
  - Parameters: short_description, description, urgency, impact, category
  - Returns: Incident number and details

- **get_incident:** Retrieve incident details by number
  - Parameters: incident_number
  - Returns: Full incident information including status, assigned_to, priority

- **update_incident:** Update existing incident
  - Parameters: incident_number, fields_to_update
  - Returns: Updated incident details

- **close_incident:** Close resolved incidents
  - Parameters: incident_number, resolution_notes
  - Returns: Closure confirmation

#### 4.2 Task Management Tools

- **assign_task:** Assign tasks to IT teams or individuals
  - Parameters: task_id, assigned_to, assignment_group
  - Returns: Assignment confirmation

- **get_my_tasks:** Retrieve tasks assigned to current user
  - Returns: List of open tasks with priorities

#### 4.3 Knowledge Base Tools

- **search_knowledge:** Search ServiceNow knowledge base
  - Parameters: search_query, category
  - Returns: Relevant knowledge articles

- **get_article:** Retrieve specific knowledge article
  - Parameters: article_id
  - Returns: Full article content

#### 4.4 Asset Management Tools

- **get_asset_info:** Retrieve IT asset information
  - Parameters: asset_tag or serial_number
  - Returns: Asset details, assignment, and status

- **request_equipment:** Submit equipment request
  - Parameters: equipment_type, justification
  - Returns: Request number

### 5. Configure Agent Behavior

1. Navigate to the **Behavior** section
2. Add or customize instructions:

```
When handling IT service requests:

For Incident Creation:
1. Gather essential information: issue description, urgency, and affected systems
2. Ask clarifying questions if details are insufficient
3. Categorize the incident appropriately (Hardware, Software, Network, etc.)
4. Set priority based on urgency and business impact
5. Provide the incident number and expected response time
6. Offer relevant knowledge articles for common issues

For Incident Status Checks:
1. Request the incident number or search by description
2. Provide current status, assigned team, and last update
3. Estimate resolution time if available
4. Offer to escalate if needed

For Knowledge Base Queries:
1. Search for relevant articles based on user's issue
2. Present top 3 most relevant articles
3. Offer to create an incident if articles don't resolve the issue
4. Track which articles are most helpful

For Asset Management:
1. Verify user identity before providing asset information
2. Track asset assignments and locations
3. Handle equipment requests with proper approvals
4. Monitor asset maintenance schedules

Always:
- Be professional and empathetic
- Provide clear incident numbers and tracking information
- Set realistic expectations for resolution times
- Escalate critical issues immediately
- Follow up on open incidents
```

### 6. Test the Agent

Test various scenarios to ensure proper functionality:

#### Test Case 1: Create an Incident
```
User: "My laptop won't connect to the VPN"
Expected Response:
- Agent asks for additional details (error messages, when it started)
- Creates incident with appropriate priority
- Provides incident number (e.g., INC0012345)
- Suggests relevant knowledge articles
- Estimates response time
```

#### Test Case 2: Check Incident Status
```
User: "What's the status of incident INC0012345?"
Expected Response:
- Retrieves incident details
- Shows current status (In Progress, Assigned, etc.)
- Displays assigned team/person
- Provides last update information
- Offers to escalate if needed
```

#### Test Case 3: Search Knowledge Base
```
User: "How do I reset my password?"
Expected Response:
- Searches knowledge base
- Presents relevant articles
- Provides step-by-step instructions
- Offers to create incident if issue persists
```

#### Test Case 4: Request Equipment
```
User: "I need a new monitor for my workstation"
Expected Response:
- Asks for justification and specifications
- Creates equipment request
- Provides request number
- Explains approval process
- Estimates delivery time
```

#### Test Case 5: Asset Information
```
User: "What's the warranty status of asset tag ABC123?"
Expected Response:
- Retrieves asset information
- Shows warranty expiration date
- Displays maintenance history
- Provides contact for support
```

### 7. Configure Notifications (Optional)

1. Navigate to **Behavior** section
2. Add notification rules:
   - Send email when high-priority incidents are created
   - Notify users of incident status changes
   - Alert on SLA breaches
   - Remind users of pending approvals

### 8. Set Up Escalation Rules

1. In the **Behavior** section, add escalation logic:

```
Escalation Rules:
- Priority 1 (Critical): Immediate escalation to IT Manager
- Priority 2 (High): Escalate if not assigned within 30 minutes
- Priority 3 (Medium): Escalate if not resolved within 4 hours
- Priority 4 (Low): Escalate if not resolved within 24 hours

Auto-escalate if:
- No response from assigned team within SLA
- User requests escalation
- Incident affects multiple users or critical systems
```

### 9. Deploy the Agent

1. Once testing is complete, click **Deploy**
2. Navigate to the **Channels** section
3. Choose deployment options:
   - **Web Chat Widget:** Embed in company intranet
   - **Slack Integration:** Connect to IT support channel
   - **Microsoft Teams:** Integrate with Teams workspace
   - **Email Integration:** Handle requests via email

### 10. Monitor and Optimize

#### 10.1 Use Agent Analytics

Track key metrics:
- Number of incidents created per day
- Average resolution time
- Most common incident categories
- Knowledge article usage
- User satisfaction scores
- Peak request times

#### 10.2 Review Performance

1. Navigate to **Analytics** dashboard
2. Monitor:
   - Incident creation trends
   - Response time metrics
   - Tool usage patterns
   - User engagement levels
   - Error rates

#### 10.3 Continuous Improvement

- Review conversation logs weekly
- Identify common issues and add to knowledge base
- Update agent behavior based on user feedback
- Add new tools as ServiceNow capabilities expand
- Train IT staff on agent capabilities

## Best Practices

### For Incident Management
- Always capture complete incident details upfront
- Set realistic expectations for resolution times
- Provide regular status updates
- Document resolutions for knowledge base
- Follow up after incident closure

### For Knowledge Base
- Keep articles up-to-date and accurate
- Use clear, non-technical language when possible
- Include screenshots and step-by-step instructions
- Track article effectiveness
- Retire outdated articles

### For Asset Management
- Verify user identity before sharing asset information
- Maintain accurate asset records
- Track asset lifecycle and maintenance
- Automate asset assignment workflows
- Monitor asset utilization

### For User Experience
- Respond promptly to all requests
- Use empathetic language
- Provide clear next steps
- Offer self-service options when appropriate
- Make escalation easy when needed

## Troubleshooting

### Issue: Agent cannot create incidents
**Solution:**
- Verify ServiceNow connection is active
- Check user permissions in ServiceNow
- Ensure required fields are being populated
- Review ServiceNow API logs

### Issue: Incident status not updating
**Solution:**
- Refresh ServiceNow connection
- Check for API rate limits
- Verify incident number format
- Ensure proper field mapping

### Issue: Knowledge articles not found
**Solution:**
- Verify knowledge base is published
- Check search permissions
- Update search keywords
- Ensure articles are categorized correctly

### Issue: Asset information unavailable
**Solution:**
- Verify asset exists in ServiceNow
- Check asset table permissions
- Ensure asset tag format is correct
- Update asset records if needed

## Integration with Other Systems

The IT Service Manager can be extended to integrate with:

- **Email Systems:** Auto-create incidents from support emails
- **Monitoring Tools:** Create incidents from system alerts
- **HR Systems:** Link to employee records for asset assignment
- **Procurement Systems:** Automate equipment ordering
- **Communication Platforms:** Send notifications via Slack/Teams

## Security Considerations

- Use secure authentication for ServiceNow connection
- Implement role-based access control
- Encrypt sensitive data in transit
- Audit all agent actions
- Comply with data privacy regulations
- Regular security reviews and updates

## Next Steps

After completing this lab, consider:
- Integrating with additional ITSM modules (Change Management, Problem Management)
- Adding custom workflows for specific incident types
- Implementing advanced analytics and reporting
- Creating specialized agents for different IT teams
- Automating routine maintenance tasks
- Building integration with monitoring and alerting systems

## Summary

You have successfully configured and deployed an IT Service Manager agent that:
- Creates and manages IT incidents through natural language
- Provides access to knowledge base articles
- Handles task assignment and routing
- Manages IT assets and equipment requests
- Integrates seamlessly with ServiceNow ITSM
- Improves IT service delivery and user satisfaction

This agent significantly reduces the burden on IT support teams while providing employees with faster, more convenient access to IT services.