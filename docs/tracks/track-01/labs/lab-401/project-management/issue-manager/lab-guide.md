# Lab guide for Issue Manager

## Overview

In this lab, you will configure and deploy a pre-built Issue Manager agent that integrates with Atlassian Jira to handle issue creation, updates, retrieval, and deletion. This agent enables development teams and project managers to interact with Jira through natural language, streamlining project management and issue tracking workflows.

## Pre-requisites

- Make sure you've already setup the environment:
- [Lab Environment setup](../../../../lab-environment-setup.md)
- Access to watsonx Orchestrate
- Atlassian Jira instance (Cloud or Server)
- Jira API token or credentials with appropriate permissions
- Basic understanding of Jira concepts (issues, projects, workflows)

## Reference Architecture

The Issue Manager follows an integrated architecture:

1. **User Interface Layer:** Chat interface where team members interact with Jira using natural language
2. **Agent Layer:** watsonx Orchestrate agent that processes requests and orchestrates Jira operations
3. **Integration Layer:** Jira REST API connections for issue management operations
4. **Jira Platform:** Backend project management system storing issues, workflows, and project data

**Key Components:**

- **Issue Manager Agent:** Pre-built agent from watsonx Orchestrate catalog
- **Jira Connector:** Authenticated connection to Jira instance
- **Issue CRUD Tools:** Create, Read, Update, Delete operations for Jira issues
- **Search and Filter Engine:** Advanced issue search and filtering capabilities
- **Workflow Management:** Handle issue transitions and status updates
- **Comment and Attachment Tools:** Add comments and manage attachments

## Steps

### 1. Access the Pre-built Agent

1. Open the watsonx Orchestrate UI
2. Navigate to the **Catalog** section
3. Search for "Jira" or "Issue Manager"
4. Click on the **Issue Manager** agent card
5. Click **Use this agent** to add it to your workspace

### 2. Configure Jira Connection

Before using the agent, establish a connection to your Jira instance.

#### 2.1 Generate Jira API Token

For Jira Cloud:
1. Log in to your Atlassian account
2. Go to **Account Settings** → **Security** → **API tokens**
3. Click **Create API token**
4. Give it a name (e.g., "watsonx Orchestrate Integration")
5. Copy the generated token (you won't be able to see it again)

For Jira Server/Data Center:
1. Use your Jira username and password
2. Or create a Personal Access Token in Jira settings

#### 2.2 Create Jira Connection in Orchestrate

1. Navigate to **Connections** in the left sidebar
2. Click **Add connection**
3. Search for "Jira" and select it
4. Enter your Jira connection details:
   - **Instance URL:** Your Jira instance URL (e.g., `https://your-company.atlassian.net`)
   - **Email/Username:** Your Jira account email or username
   - **API Token/Password:** The API token you generated
   - **Connection Name:** "Jira Project Management"

5. Click **Test connection** to verify connectivity
6. Click **Save** once the test is successful

#### 2.3 Link Connection to Agent

1. Open the **Issue Manager** agent in Agent Builder
2. Navigate to the **Toolset** section
3. For each Jira tool, click the settings icon
4. Select the Jira connection you created
5. Click **Save**

### 3. Configure Agent Profile

1. In the **Profile** section, review and customize:
   - **Purpose:** "Assist teams with Jira issue management through natural language interactions"
   - **Usage Scenarios:** "Use this agent for creating issues, updating status, searching issues, and managing project tasks"
   - **Interaction Style:** Keep as **Default** for natural conversation flow

### 4. Review Available Tools

The pre-built agent includes the following tools:

#### 4.1 Issue Creation Tools

- **create_issue:** Create new Jira issues
  - Parameters: project_key, issue_type, summary, description, priority, assignee
  - Returns: Issue key (e.g., PROJ-123) and details

- **create_subtask:** Create subtasks under parent issues
  - Parameters: parent_issue_key, summary, description, assignee
  - Returns: Subtask key and details

#### 4.2 Issue Retrieval Tools

- **get_issue:** Retrieve issue details by key
  - Parameters: issue_key
  - Returns: Complete issue information including status, assignee, comments, attachments

- **search_issues:** Search issues using JQL or natural language
  - Parameters: search_query, project, status, assignee, max_results
  - Returns: List of matching issues

- **get_my_issues:** Retrieve issues assigned to current user
  - Parameters: status_filter (optional)
  - Returns: List of assigned issues

- **get_project_issues:** Get all issues in a project
  - Parameters: project_key, status_filter
  - Returns: List of project issues

#### 4.3 Issue Update Tools

- **update_issue:** Update issue fields
  - Parameters: issue_key, fields_to_update (summary, description, priority, assignee, etc.)
  - Returns: Updated issue details

- **transition_issue:** Move issue through workflow
  - Parameters: issue_key, transition_name (e.g., "In Progress", "Done")
  - Returns: New issue status

- **assign_issue:** Assign issue to team member
  - Parameters: issue_key, assignee_username
  - Returns: Assignment confirmation

- **update_priority:** Change issue priority
  - Parameters: issue_key, priority (Highest, High, Medium, Low, Lowest)
  - Returns: Updated priority

#### 4.4 Issue Deletion Tools

- **delete_issue:** Delete an issue
  - Parameters: issue_key, delete_subtasks (boolean)
  - Returns: Deletion confirmation

#### 4.5 Comment and Collaboration Tools

- **add_comment:** Add comment to issue
  - Parameters: issue_key, comment_text, visibility (optional)
  - Returns: Comment ID

- **get_comments:** Retrieve all comments on an issue
  - Parameters: issue_key
  - Returns: List of comments with authors and timestamps

- **link_issues:** Link related issues
  - Parameters: issue_key, related_issue_key, link_type
  - Returns: Link confirmation

#### 4.6 Attachment Tools

- **add_attachment:** Upload file to issue
  - Parameters: issue_key, file_path
  - Returns: Attachment ID

- **get_attachments:** List issue attachments
  - Parameters: issue_key
  - Returns: List of attachments with download links

### 5. Configure Agent Behavior

1. Navigate to the **Behavior** section
2. Add or customize instructions:

```
When managing Jira issues:

For Issue Creation:
1. Gather essential information: project, issue type, summary, and description
2. Ask for priority and assignee if not specified
3. Validate project key exists
4. Confirm issue type is valid for the project
5. Create the issue and provide the issue key
6. Offer to add additional details (labels, components, custom fields)

For Issue Updates:
1. Verify the issue key exists
2. Confirm what fields need to be updated
3. Validate new values are appropriate
4. Apply updates and confirm changes
5. Notify relevant stakeholders if needed

For Issue Search:
1. Understand the search criteria (project, status, assignee, keywords)
2. Use JQL for complex queries when appropriate
3. Present results in a clear, organized format
4. Offer to filter or refine results
5. Provide quick actions for each result (view, update, comment)

For Workflow Transitions:
1. Check current issue status
2. Verify the requested transition is valid
3. Prompt for required fields if any
4. Execute the transition
5. Confirm the new status

For Comments and Collaboration:
1. Add comments with proper formatting
2. Mention team members using @username
3. Support rich text formatting (bold, italic, lists, code blocks)
4. Respect comment visibility settings
5. Notify mentioned users

Always:
- Use clear, concise language
- Provide issue keys for easy reference
- Respect project permissions and workflows
- Handle errors gracefully with helpful suggestions
- Maintain context across conversation
- Offer relevant next actions
```

### 6. Test the Agent

Test various scenarios to ensure proper functionality:

#### Test Case 1: Create a Bug Issue
```
User: "Create a bug in project DEMO: Login button not working on mobile devices"
Expected Response:
- Agent asks for additional details (priority, assignee, steps to reproduce)
- Creates the bug issue
- Returns issue key (e.g., DEMO-456)
- Offers to add attachments or screenshots
```

#### Test Case 2: Search for Issues
```
User: "Show me all high priority bugs assigned to John in the DEMO project"
Expected Response:
- Searches using appropriate filters
- Displays list of matching issues with key details
- Provides quick actions for each issue
- Offers to refine search if needed
```

#### Test Case 3: Update Issue Status
```
User: "Move DEMO-456 to In Progress"
Expected Response:
- Verifies issue exists
- Checks if transition is valid
- Executes the transition
- Confirms new status
- Shows updated issue details
```

#### Test Case 4: Add Comment
```
User: "Add a comment to DEMO-456: Fixed the CSS issue, ready for testing"
Expected Response:
- Adds the comment to the issue
- Confirms comment was added
- Shows comment ID and timestamp
- Offers to notify team members
```

#### Test Case 5: Bulk Operations
```
User: "Assign all open bugs in DEMO project to Sarah"
Expected Response:
- Searches for matching issues
- Shows list of issues to be updated
- Asks for confirmation
- Executes bulk assignment
- Provides summary of changes
```

#### Test Case 6: Get My Issues
```
User: "What issues are assigned to me?"
Expected Response:
- Retrieves issues assigned to current user
- Groups by status or priority
- Shows key details for each issue
- Offers to update or comment on issues
```

### 7. Configure Advanced Features

#### 7.1 Custom Fields Support

1. Navigate to **Toolset** section
2. For each tool, configure custom field mappings
3. Add project-specific custom fields:
   - Story Points
   - Sprint
   - Epic Link
   - Custom dropdowns
   - Custom text fields

#### 7.2 Workflow Automation

Add automated workflows:
```
Automation Rules:
- Auto-assign issues based on component or label
- Auto-transition issues when all subtasks are complete
- Auto-add watchers based on issue type
- Auto-set due dates based on priority
- Auto-create subtasks for specific issue types
```

#### 7.3 Notification Settings

Configure notifications:
- Notify assignee when issue is created
- Alert watchers on status changes
- Send daily digest of assigned issues
- Notify on approaching due dates
- Alert on priority changes

### 8. Deploy the Agent

1. Once testing is complete, click **Deploy**
2. Navigate to the **Channels** section
3. Choose deployment options:
   - **Web Chat Widget:** Embed in project portal or wiki
   - **Slack Integration:** Connect to development team channels
   - **Microsoft Teams:** Integrate with project Teams workspace
   - **Email Integration:** Create issues from email
   - **IDE Integration:** Access from development environment

### 9. Monitor and Optimize

#### 9.1 Use Agent Analytics

Track key metrics:
- Number of issues created per day
- Most common issue types
- Average time to resolution
- User adoption rates
- Tool usage patterns
- Search query patterns

#### 9.2 Review Performance

1. Navigate to **Analytics** dashboard
2. Monitor:
   - Issue creation trends
   - Status transition patterns
   - Team workload distribution
   - Response time metrics
   - Error rates and types

#### 9.3 Continuous Improvement

- Review conversation logs weekly
- Identify common queries and optimize responses
- Add shortcuts for frequent operations
- Update behavior based on team feedback
- Expand tool coverage as needs evolve
- Train team on advanced features

## Best Practices

### For Issue Creation
- Use clear, descriptive summaries
- Provide detailed descriptions with context
- Set appropriate priority levels
- Assign to the right team member
- Add relevant labels and components
- Link related issues

### For Issue Management
- Keep issues up-to-date
- Transition issues promptly
- Add meaningful comments
- Update estimates and time tracking
- Close completed issues
- Archive old issues

### For Search and Filtering
- Use specific search criteria
- Leverage JQL for complex queries
- Save frequently used filters
- Use labels for categorization
- Maintain consistent naming conventions
- Regular cleanup of stale issues

### For Team Collaboration
- Mention team members in comments
- Use @mentions for notifications
- Share issue links in discussions
- Document decisions in comments
- Keep stakeholders informed
- Respect notification preferences

## Troubleshooting

### Issue: Agent cannot create issues
**Solution:**
- Verify Jira connection is active
- Check user permissions in Jira
- Ensure project key is correct
- Verify issue type is valid for project
- Check required fields are populated

### Issue: Search returns no results
**Solution:**
- Verify search criteria
- Check project permissions
- Ensure issues exist matching criteria
- Try broader search terms
- Check JQL syntax if using advanced search

### Issue: Cannot transition issue
**Solution:**
- Verify current issue status
- Check workflow configuration
- Ensure transition is valid from current status
- Verify user has permission to transition
- Check for required fields in transition

### Issue: Comments not appearing
**Solution:**
- Verify comment was added successfully
- Check comment visibility settings
- Ensure user has permission to view comments
- Refresh issue view
- Check Jira audit log

## Integration with Development Tools

The Issue Manager can be extended to integrate with:

- **Git/GitHub/GitLab:** Link commits and pull requests to issues
- **CI/CD Pipelines:** Auto-update issues based on build status
- **Code Review Tools:** Create issues from code review comments
- **Testing Tools:** Auto-create bugs from failed tests
- **Monitoring Tools:** Create incidents from alerts
- **Documentation Tools:** Link issues to documentation

## Advanced Use Cases

### Sprint Planning
```
User: "Show me all unassigned stories in the backlog"
Agent: Lists unassigned stories
User: "Assign the top 5 to the current sprint"
Agent: Moves issues to sprint and confirms
```

### Release Management
```
User: "List all issues in version 2.0 that are not done"
Agent: Shows incomplete issues for release
User: "Move all low priority issues to version 2.1"
Agent: Bulk updates fix version
```

### Bug Triage
```
User: "Show me all new bugs from the last 24 hours"
Agent: Lists recent bugs
User: "Set priority to high for bugs with 'critical' in the title"
Agent: Bulk updates priorities
```

## Security Considerations

- Use API tokens instead of passwords
- Implement role-based access control
- Audit all agent actions
- Encrypt credentials in transit and at rest
- Regular security reviews
- Comply with data privacy regulations
- Monitor for suspicious activity
- Implement rate limiting

## Next Steps

After completing this lab, consider:
- Integrating with additional Atlassian tools (Confluence, Bitbucket)
- Creating custom workflows for specific project types
- Implementing advanced automation rules
- Building integration with development tools
- Creating specialized agents for different teams
- Implementing advanced reporting and analytics
- Adding AI-powered issue recommendations

## Summary

You have successfully configured and deployed an Issue Manager agent that:
- Creates, updates, retrieves, and deletes Jira issues through natural language
- Provides efficient search and filtering capabilities
- Handles workflow transitions and status updates
- Manages comments, attachments, and collaboration
- Integrates seamlessly with Atlassian Jira
- Improves team productivity and project management efficiency

This agent significantly reduces the complexity of Jira usage while providing powerful issue management capabilities to all team members, regardless of their technical expertise.