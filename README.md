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
                              Manual Review ← Form Responses (Excel/Forms Dashboard)
```

## Email Domains Monitored
- `no-reply@expert.onthemarket.com`
- `autoresponder@rightmove.com`
- `members@zoopla.co.uk`

### Pre-Populated Fields (via URL parameters)
- Applicant Name (from email extraction)
- Email Address (from email extraction)
- Property Address (from email extraction)
- Property Reference (from email extraction)
