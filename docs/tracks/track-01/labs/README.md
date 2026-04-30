# Lab Structure Overview

## Use Case-Based Lab Organization

The labs have been restructured to support multiple use cases per domain. Each lab (101, 201, 301, 401) now includes domain-specific use cases that participants can choose based on their interests.

### Structure

```
lab-XXX/
├── index.md                           # Lab introduction with domain selection
├── prerequisites.md                   # General prerequisites
└── [domain]/
    ├── index.md                      # Domain overview with use case selection
    └── use-case-N/
        ├── details.md                # Use case business context and requirements
        └── lab-guide.md              # Step-by-step implementation guide
```

### Available Domains

1. **Retail** - E-commerce, inventory management, customer experience
2. **Legal** - Contract management, legal research, compliance tracking
3. **Automobile** - Vehicle management, dealership operations, service scheduling
4. **Financial Services** - Banking operations, investment management, risk assessment
5. **Insurance** - Policy management, claims processing, risk assessment
6. **Marketing** - Campaign management, customer analytics, content optimization

### Use Case Structure

Each domain contains **2 use cases** that provide different business scenarios while teaching the same technical concepts:

#### Use Case Files

1. **details.md** - Business context and requirements
   - Business challenge description
   - Solution overview
   - Expected outcomes
   - Technical components
   - Prerequisites

2. **lab-guide.md** - Implementation guide
   - Step-by-step instructions
   - Code examples and schemas
   - Validation criteria
   - Troubleshooting tips

### Learning Path

Participants follow this workflow:

1. **Start at Lab Introduction** (`lab-XXX/index.md`)
   - Review what they'll build
   - Understand learning objectives
   - Check estimated duration
   - Review prerequisites
   - **Select their domain of interest**

2. **Navigate to Domain Overview** (`lab-XXX/[domain]/index.md`)
   - Understand domain-specific context
   - Review available use cases
   - **Select a use case to implement**

3. **Follow Use Case Content**
   - **Details**: Understand the business scenario and requirements
   - **Lab Guide**: Complete hands-on implementation

4. **Progress Through Labs**
   - Lab 101: Basics (2 use cases per domain)
   - Lab 201: Fundamentals (2 use cases per domain)
   - Lab 301: Intermediate (2 use cases per domain)
   - Lab 401: Advanced (2 use cases per domain)

### Example: Lab 101 - Retail Domain

```
lab-101/retail/
├── index.md                          # Retail domain overview
├── use-case-1/
│   ├── details.md                   # E-Commerce Product Catalog
│   └── lab-guide.md                 # Implementation guide
└── use-case-2/
    ├── details.md                   # Omnichannel Inventory Management
    └── lab-guide.md                 # Implementation guide
```

### Benefits

- **Flexibility**: Multiple use cases per domain allow participants to choose scenarios that match their interests
- **Relevance**: Industry-specific scenarios increase engagement and learning effectiveness
- **Consistency**: All use cases within a lab level cover the same technical concepts
- **Scalability**: Easy to add new use cases without restructuring
- **Focused Learning**: Simplified structure with just 2 files per use case (details + lab guide)

### Navigation Hierarchy

The MkDocs navigation reflects this structure:

```yaml
- Labs:
  - Lab 101 — Basics:
    - Introduction
    - Prerequisites
    - Domains:
      - Retail:
        - Overview
        - Use Cases:
          - E-Commerce Product Catalog:
            - Details
            - Lab Guide
          - Omnichannel Inventory:
            - Details
            - Lab Guide
      - [Other domains...]
```

### Content Customization

Each use case should include:

**Details Page:**
- Business context and challenges
- Solution overview
- Expected business outcomes
- Technical components list
- Estimated duration
- Prerequisites

**Lab Guide Page:**
- Step-by-step implementation instructions
- Code examples and schemas
- Expected outputs for each step
- Validation and testing procedures
- Troubleshooting guidance
- Next steps and resources

### Adding New Use Cases

To add a new use case to a domain:

1. Create a new directory: `lab-XXX/[domain]/use-case-N/`
2. Add `details.md` with business context
3. Add `lab-guide.md` with implementation steps
4. Update `lab-XXX/[domain]/index.md` to include the new use case card
5. Update `mkdocs.yml` navigation to include the new use case

### Maintenance Notes

- Old `overview.md`, `steps.md`, `validation.md`, and `recap.md` files can be removed once all content is migrated to the new structure
- Each domain's `index.md` serves as the use case selection page
- Use case names should be descriptive and business-focused
- Lab guides should be self-contained with all necessary information
- Maintain consistent formatting across all use cases

### File Naming Convention

- Domain overview: `[domain]/index.md`
- Use case details: `[domain]/use-case-N/details.md`
- Use case lab guide: `[domain]/use-case-N/lab-guide.md`

Where N is a sequential number (1, 2, 3, etc.)