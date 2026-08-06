---
name: 11x
description: Use when building, testing, or deploying browser automation workflows, RPA tasks, or AI-powered agents that interact with web applications. Reach for this skill when you need to create automated workflows, configure integrations, manage executions, or troubleshoot automation issues.
metadata:
    mintlify-proj: 11x
    version: "1.0"
---

# 11x Skill Reference

## Product summary

11x is an AI-powered browser automation and RPA (Robotic Process Automation) platform that enables agents to build, execute, and manage automated workflows that interact with web applications. Agents use 11x to create intelligent automation tasks without writing code, configure integrations with external systems, monitor execution runs, and handle complex business processes. The platform provides a visual workflow builder, API access for programmatic control, and execution management through a web dashboard. Key resources: primary documentation at https://docs.11x.ai, comprehensive page listing at https://docs.11x.ai/llms.txt.

## When to use

Reach for this skill when:
- **Building workflows**: Creating new automation tasks that interact with web applications, forms, or APIs
- **Configuring integrations**: Setting up connections between 11x and external systems (CRM, ERP, databases, webhooks)
- **Managing executions**: Monitoring, triggering, or debugging automation runs
- **Troubleshooting failures**: Diagnosing why workflows failed, fixing broken steps, or optimizing performance
- **Testing automation**: Validating workflow logic before deploying to production
- **Scaling operations**: Deploying workflows across multiple environments or scheduling recurring tasks
- **Handling edge cases**: Implementing error handling, retries, or conditional logic in workflows

Do not use this skill for: general web development, building traditional applications, or tasks that don't involve browser automation or RPA.

## Quick reference

### Core concepts
| Concept | Definition |
|---------|-----------|
| **Workflow** | A sequence of automated steps that interact with web applications or APIs |
| **Step** | An individual action within a workflow (click, type, extract data, API call) |
| **Execution** | A single run of a workflow with specific inputs and outputs |
| **Agent** | An AI-powered entity that can autonomously execute workflows or make decisions |
| **Integration** | A connection between 11x and external systems (webhooks, APIs, databases) |
| **Trigger** | An event that initiates a workflow (manual, scheduled, webhook, API call) |

### Common workflow actions
- **Browser actions**: Click element, type text, navigate URL, wait for element, extract text/data
- **Data operations**: Transform data, validate inputs, format outputs, merge datasets
- **API calls**: Send HTTP requests, handle responses, parse JSON
- **Conditional logic**: If/then branches, loops, error handling
- **Integration actions**: Send to external system, receive data from webhook, query database

### API endpoints (typical structure)
```
POST /api/workflows/{id}/execute     # Trigger workflow execution
GET /api/executions/{id}             # Get execution status/results
POST /api/integrations               # Create integration
GET /api/workflows                   # List workflows
```

### Authentication
- Use API keys for programmatic access
- Include key in request headers: `Authorization: Bearer YOUR_API_KEY`
- Rotate keys regularly; never commit keys to version control

## Decision guidance

### When to use visual builder vs API
| Scenario | Use visual builder | Use API |
|----------|-------------------|---------|
| Creating new workflows | ✓ | |
| Testing workflow logic | ✓ | |
| Triggering workflows from external systems | | ✓ |
| Bulk creating similar workflows | | ✓ |
| Monitoring executions programmatically | | ✓ |
| Quick prototyping | ✓ | |

### When to use different trigger types
| Trigger type | Best for | Example |
|--------------|----------|---------|
| **Manual** | Testing, one-off tasks | Run workflow on demand from dashboard |
| **Scheduled** | Recurring tasks | Daily data sync at 2 AM |
| **Webhook** | Event-driven automation | Trigger when form submitted |
| **API call** | System integration | Trigger from external application |

### When to use error handling strategies
| Strategy | Use when | Example |
|----------|----------|---------|
| **Retry** | Transient failures likely | Network timeout, temporary API unavailability |
| **Skip step** | Step is optional | Optional data enrichment |
| **Fallback value** | Default behavior acceptable | Use cached data if API fails |
| **Stop workflow** | Failure is critical | Missing required data, authentication failed |

## Workflow

### Typical task: Build and deploy a new automation workflow

1. **Understand requirements**
   - Identify the web application or system to automate
   - List all steps the workflow must perform
   - Define inputs (what data the workflow receives)
   - Define outputs (what data the workflow produces)
   - Identify error scenarios and how to handle them

2. **Check existing workflows**
   - Search dashboard for similar workflows
   - Review existing integrations that might be reused
   - Check if workflow already exists (avoid duplicates)

3. **Create workflow in visual builder**
   - Start with a blank workflow
   - Add steps in sequence: navigate, interact, extract, transform
   - Use conditional logic for branching
   - Add error handling for each critical step
   - Test with sample data

4. **Configure integrations**
   - Connect to external systems (CRM, database, webhook)
   - Map workflow outputs to integration inputs
   - Test integration connection before deploying

5. **Set up triggers**
   - Choose trigger type (manual, scheduled, webhook, API)
   - Configure trigger parameters (schedule, webhook URL, API endpoint)
   - Document how external systems should invoke the workflow

6. **Test thoroughly**
   - Run workflow with test data
   - Verify all outputs are correct
   - Test error scenarios (missing data, network failures)
   - Check integration data reaches external systems

7. **Deploy to production**
   - Enable workflow in production environment
   - Monitor first few executions
   - Set up alerts for failures

8. **Monitor and maintain**
   - Review execution logs regularly
   - Track success/failure rates
   - Update workflow if target application changes

### Typical task: Troubleshoot a failing workflow

1. **Identify the failure**
   - Check execution logs in dashboard
   - Note which step failed and error message
   - Check if failure is consistent or intermittent

2. **Diagnose root cause**
   - Review step configuration (selectors, API endpoints, data mapping)
   - Check if target application changed (UI update, API change)
   - Verify integrations are still connected
   - Check if input data is valid

3. **Fix the issue**
   - Update step configuration (new selectors, corrected API call)
   - Add error handling if missing
   - Adjust timeouts if application is slow
   - Update integration credentials if expired

4. **Test the fix**
   - Run workflow with same data that caused failure
   - Verify workflow completes successfully
   - Check outputs are correct

5. **Deploy fix**
   - Update production workflow
   - Monitor next executions

## Common gotchas

- **Brittle selectors**: Web element selectors break when UI changes. Use stable selectors (IDs, data attributes) instead of position-based selectors. Test selectors regularly.

- **Timing issues**: Workflows fail if they interact with elements before they load. Add explicit waits for elements to appear, don't rely on fixed delays.

- **Missing error handling**: Workflows stop abruptly if a step fails without error handling. Add error handlers to every critical step (API calls, data extraction, integrations).

- **Hardcoded values**: Workflows fail when hardcoded values change (URLs, account IDs, dates). Use workflow inputs and variables instead.

- **Stale integrations**: External system credentials expire or change. Regularly verify integration connections work, rotate API keys, update credentials promptly.

- **Data type mismatches**: Workflows fail when data types don't match (string vs number, date format). Validate and transform data explicitly.

- **Unhandled edge cases**: Workflows work for happy path but fail on edge cases (empty results, special characters, null values). Test with realistic data including edge cases.

- **Performance issues**: Workflows timeout if they're too slow. Optimize by removing unnecessary steps, parallelizing where possible, increasing timeouts for slow applications.

- **Incorrect variable scope**: Variables defined in one step aren't available in another. Understand variable scope and pass data explicitly between steps.

- **API rate limits**: Workflows fail when hitting external API rate limits. Add delays between API calls, implement exponential backoff, check rate limit documentation.

## Verification checklist

Before submitting a workflow for production use:

- [ ] Workflow executes successfully with test data
- [ ] All required inputs are defined and documented
- [ ] All outputs are correct and properly formatted
- [ ] Error handling is in place for all critical steps
- [ ] Integrations are tested and credentials are valid
- [ ] Selectors/locators are stable and won't break on UI changes
- [ ] Workflow handles edge cases (empty data, special characters, null values)
- [ ] Performance is acceptable (no unnecessary delays or timeouts)
- [ ] Trigger is configured correctly (schedule, webhook, API endpoint)
- [ ] Logs are clear and help diagnose failures
- [ ] Documentation describes what workflow does and how to use it
- [ ] Workflow has been tested in staging environment
- [ ] Monitoring/alerts are configured for production

## Resources

- **Comprehensive documentation**: https://docs.11x.ai/llms.txt — page-by-page navigation of all 11x documentation
- **API Reference**: https://docs.11x.ai/api — detailed API endpoints, request/response formats, authentication
- **Workflow Builder Guide**: https://docs.11x.ai/workflows — how to build workflows, available actions, best practices
- **Integration Setup**: https://docs.11x.ai/integrations — connecting to external systems, webhook configuration, credential management

---

> For additional documentation and navigation, see: https://docs.11x.ai/llms.txt