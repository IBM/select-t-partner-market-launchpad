# Lab guide for Flight Booking Assistant

## Overview

In this lab, you will create an agentic workflow (previously known as flow) that uses forms to book a flight. You will guide users through a series of questions to collect travel details including departure city, arrival city, trip type, dates, ticket class, number of travellers, and booking confirmation. The agentic workflow will analyze these inputs, suggest available flights, use branching conditions to determine whether to proceed with booking, and generate a summary message using logic blocks. This lab demonstrates how to create forms in user activities and how configured prompts appear in the chat interface.

## Pre-requisites

- Make sure you've already setup the environment:
- [Lab Environment setup](../../../../lab-environment-setup.md)
- Access to watsonx Orchestrate
- Basic understanding of REST APIs and OpenAPI specifications

## Reference Architecture

The Flight Booking Assistant follows an agentic workflow architecture:

1. **User Interface Layer:** Form-based chat interface where users provide travel details through guided questions
2. **Workflow Layer:** Agentic workflow that orchestrates the booking process using user activities and logic blocks
3. **User Activities:** Form inputs that collect travel information (departure city, arrival city, trip type, dates, class, travellers, booking confirmation)
4. **Logic Blocks:** Process user inputs and generate flight suggestions and booking summaries
5. **Branching Conditions:** Determine workflow paths based on user responses (e.g., whether to proceed with booking)

**Key Components:**

- **Form-Based User Activities:** Structured inputs for collecting travel details
- **Flight Suggestion Logic:** Analyzes user inputs to present available flight options
- **Branching Logic:** Conditional workflow paths based on booking confirmation
- **Summary Generation:** Creates booking confirmation messages using logic blocks

## Steps

### 1. Import the Flight Booking Agent

- Run the import script to load the pre-configured flight booking agent:

```bash
./import-all.sh
```

This script will import the `book_a_flight_agent` with all the necessary configurations, including:

- Form-based user activities for collecting travel details
- Logic blocks for flight suggestions and booking summaries
- Branching conditions for handling booking confirmation
- Multi-turn conversation flow

### 2. Launch the Chat UI

- Start the watsonx Orchestrate chat interface:

```bash
orchestrate chat start
```

This will launch the chat UI where you can interact with the flight booking agent.

### 3. Select the Flight Booking Agent

- In the chat interface, select the **book_a_flight_agent** from the available agents list.

### 4. Test the Flight Booking Workflow

1. Type a natural language request to book a flight. For example:
   ```
   book a flight from london to the big apple leaving tomorrow returning on Friday for me and my wife
   ```

1. The agentic workflow will guide you through the flight booking process by presenting a sequence of forms and multi-turn user activities in the chat, including:
     - Departure city selection (single choice)
     - Arrival city selection (single choice)
     - Trip type selection (single choice)
     - Departure date (date input)
     - Return date (date input)
     - Ticket class selection (single choice)
     - Number of travellers (number input)
     - Flight selection from suggested options
     - Booking confirmation (boolean)

1. Follow the prompts and provide the requested information through the form-based interface.

1. The workflow will analyze your inputs, suggest available flights, and guide you through the booking confirmation process.

1. Upon completion, you'll receive a booking summary with all travel details and a confirmation reference.

### 5. Building the workflows

Watch this video to learn how to build the workflow step by step:

<div markdown="1">
<iframe
  src="https://cdnapisec.kaltura.com/p/1773841/embedPlaykitJs/uiconf_id/27941801?iframeembed=true&entry_id=1_0vcwyy5g"
  width="720"
  height="405"
  allowfullscreen
  style="border: none;">
</iframe>
</div>

## Best Practices

- **Use clear and concise prompts** in form questions to guide users effectively
- **Provide relevant options** in single-choice fields based on common travel patterns
- **Validate date inputs** to ensure departure dates are before return dates
- **Show conditional fields** only when relevant (e.g., return date for round-trips)
- **Present flight options clearly** with key details like price, duration, and stops
- **Use branching logic** to handle different user decisions efficiently
- **Generate comprehensive summaries** that confirm all booking details
- **Test all workflow paths** including booking confirmation and cancellation

## Troubleshooting

**Issue:** Form fields not appearing correctly
- Verify user activity configuration
- Check conditional logic for dependent fields
- Ensure variable names are correctly referenced

**Issue:** Branching condition not working
- Verify boolean variable is correctly captured
- Check condition syntax in branching block
- Test both true and false paths

**Issue:** Summary message missing information
- Verify all variables are correctly referenced in logic block
- Check that user inputs are being stored properly
- Ensure variable names match between activities and logic blocks

**Issue:** Flight suggestions not displaying
- Verify logic block configuration
- Check that all required inputs are collected
- Ensure flight data is properly formatted

## Next Steps

After completing this lab, consider:
- Adding seat selection as an additional user activity
- Integrating meal preferences and special requests
- Implementing multi-city trip support with additional form fields
- Adding payment processing workflow steps
- Creating email confirmation logic blocks
- Integrating with calendar systems for automatic event creation

## Summary

You have successfully created a Flight Booking agentic workflow that:
- Guides users through a structured form-based booking process
- Collects travel details using various input types (single choice, date, number, boolean)
- Analyzes user inputs to suggest available flights
- Uses branching conditions to handle booking confirmation or cancellation
- Generates comprehensive booking summaries using logic blocks
- Demonstrates how forms in user activities appear in the chat interface

This form-based approach provides a guided, structured experience that ensures all necessary information is collected efficiently while maintaining a conversational interface.