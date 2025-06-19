# Estate Agency Application Automation Project

## Problem Statement

Our letting estate agency receives numerous inquiries from property listing platforms (OnTheMarket, Rightmove, Zoopla, etc.) where applicants often don't meet basic requirements:
- Income too low for the property
- Want to bring pets to no-pet properties
- Move-in dates that don't align with availability
- Other basic qualification mismatches

**Current Impact:** Significant time wasted reviewing unqualified applications manually.

## Solution Overview

Implement an automated screening system that filters applicants before manual review, using Microsoft's ecosystem for seamless integration with existing Outlook workflow.

### Key Components
- **Trigger:** Incoming emails from listing platforms
- **Screening:** Microsoft Forms with validation logic
- **Automation:** Power Automate for conditional responses
- **Management:** Integration with SMEprofessional property management system

## Technical Architecture

```
OnTheMarket/Rightmove/Zoopla Email → Power Automate Trigger → Extract Applicant Email → Send Form Directly to Applicant
                                                      ↓
                                Response Validation ← Form Submission
                                                      ↓
                                            Conditional Email Response
```

## Solution: Power Automate + Microsoft Forms

**Features:**
- Automatic email parsing to extract applicant contact details
- Direct communication with applicants (bypassing platform)
- Conditional email responses based on form answers
- Automatic lead scoring and qualification
- Integration with SharePoint/Excel for tracking
- Teams notifications for qualified applicants

## Email Domains to Monitor
- `no-reply@expert.onthemarket.com`
- `autoresponder@rightmove.com`
- `members@zoopla.co.uk`

## Power Automate Email Parsing

**Automatic Extraction:**
Power Automate will parse incoming emails to extract:
- Applicant name (e.g., "Lee Mccarroll")
- Applicant email address
- Property details/address
- Inquiry type

**Direct Contact:**
Instead of replying to the platform, Power Automate sends the screening form directly to the applicant's email address, creating a more personal and professional experience.

## Form Validation Logic

### Income Requirements
```
IF monthly_income < property_minimum_income:
    → Send rejection email with alternative properties
    → Flag as "Income Insufficient" in tracking
```

### Pet Policy Validation
```
IF has_pets = "Yes" AND property_allows_pets = "No":
    → Send rejection email with pet-friendly alternatives
    → Provide list of available pet-friendly properties
```

### Availability Matching
```
IF move_in_date > property_available_date:
    → Send email with actual availability
    → Suggest similar properties available sooner
```

### Qualified Applicant Flow
```
IF all_requirements_met = True:
    → Send priority response with next steps
    → Notify team via Teams/email
    → Auto-schedule or provide booking link
    → Update tracking spreadsheet with priority flag
```

## Implementation Steps

- [ ] Contact SMEprofessional about API/webhook capabilities
- [ ] Set up basic Outlook rule for auto-replies
- [ ] Create Microsoft Form with key screening questions
- [ ] Design conditional logic for different scenarios
- [ ] Set up response email templates
- [ ] Build Power Automate flow connecting Outlook → Forms → Conditional Responses
- [ ] Test validation rules with sample inquiries
- [ ] Test end-to-end workflow
- [ ] Train team on new process
- [ ] Implement SMEprofessional integration (if available)
- [ ] Set up qualified applicant routing

## Form Questions Template

### Basic Information
- Property of interest (dropdown)
- Desired move-in date
- Monthly gross income
- Employment status

### Qualification Screening
- Do you have pets? (If yes → specify type/number)
- Previous rental references available?
- Reason for moving
- Any special requirements?

### Property-Specific Validation
- Income verification (minimum 3x rent)
- Pet policy compliance
- Move-in date feasibility
- Background check consent

## Email Response Templates

### Qualified Applicant
```
Subject: Great News! You Meet Our Requirements

Hi [Name],

Excellent news! Based on your responses, you meet the basic requirements for [Property Address].

Next Steps:
1. Schedule a viewing: [Booking Link]
2. Complete full application: [Application Link]
3. Expect contact within 24 hours

We look forward to hearing from you!
```

### Income Insufficient
```
Subject: Alternative Properties Available

Hi [Name],

Thank you for your interest in [Property Address]. Based on our requirements, we recommend properties in your budget range:

[List of suitable alternatives]

Feel free to apply for any of these options!
```

### Pet Policy Mismatch
```
Subject: Pet-Friendly Properties Available

Hi [Name],

While [Property Address] doesn't allow pets, we have several pet-friendly options:

[List of pet-friendly properties]

Your furry friends are welcome at these locations!
```

## Technical Requirements

- Outlook with rule creation access
- Power Automate license (free tier sufficient initially)
- Microsoft Forms access
