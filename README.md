# QA Skills Project

A comprehensive skill-based system for Senior QA Engineers covering the entire software testing lifecycle.

## Overview

This project implements an orchestrator-driven approach where a master coordinator delegates work to specialized QA skills. Every task goes through the orchestrator, which identifies required skills, searches for missing ones, and coordinates execution.

## Architecture

```
User Request
    ↓
senior-qa-engineer (Main Coordinator)
    ↓
multi-agent-orchestration (Master Orchestrator)
    ↓
Specialized Skills (by QA Phase)
    ↓
Results Aggregation & Delivery
```

## Core Skills

### Main Entry Point
- **senior-qa-engineer** (`SKILL.md`): Master coordinator that defines the QA role and workflow

### Master Orchestrator
- **multi-agent-orchestration**: Coordinates all task execution, manages skill discovery and workflow

### QA Lifecycle Skills

#### Phase 1: Requirements & Planning
- **user-story-verifier**: Validates user stories for quality, completeness, INVEST criteria, and ISTQB applicability

#### Phase 2: Test Design
- **test-design-istqb**: Applies ISTQB techniques (equivalence partitioning, boundary values, decision tables, state transitions) to create test cases

#### Phase 3: Test Execution
- **test-execution-manager**: Manages test execution, defect logging, exploratory testing, and status reporting

#### Phase 4: Defect Management
- **defect-lifecycle-manager**: Tracks defects through their lifecycle, analyzes metrics, performs root cause analysis

#### Phase 5: CI/CD & Automation
- **cicd-testing-integration**: Integrates tests into CI/CD pipelines, enables continuous testing
- **browser-use**: Automates browser interactions for web testing

#### Phase 6: Continuous Improvement
- **qa-process-improvement**: Drives process optimization through metrics analysis and best practices

### Utility Skills
- **skill-creator**: Creates new specialized skills when needed
- **find-skills**: Searches the skills ecosystem for capabilities

## How It Works

### 1. Request Received
User makes a QA-related request (e.g., "Review this user story" or "Create automated tests")

### 2. Orchestrator Activated
The **multi-agent-orchestration** skill is ALWAYS activated first. It:
- Analyzes the request
- Identifies which QA phase(s) are involved
- Determines required skills
- Plans execution pattern (sequential/parallel/hierarchical)

### 3. Skill Discovery
For each required skill:
- **Exists locally?** → Queue for execution
- **Not found?** → Use **find-skills** to search ecosystem
  - Found? → Ask user to install
  - Not found? → Use **skill-creator** to propose new skill

### 4. Execution
Orchestrator runs skills in planned order:
- Sequential: A → B → C (when output of A feeds B)
- Parallel: A + B + C (when independent tasks)
- Hierarchical: Orchestrator → Sub-tasks → Aggregation

### 5. Aggregation & Delivery
Orchestrator combines results and delivers comprehensive response to user

## Mandatory Workflow

```
┌─────────────────────────────────────┐
│ 1. User Request                     │
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│ 2. Activate multi-agent-orchestration│
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│ 3. Analyze & Plan                   │
│    - What phase?                    │
│    - Which skills needed?           │
│    - Execution pattern?             │
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│ 4. For each skill needed:           │
│    - Check inventory                │
│    - Search if missing              │
│    - Create if unavailable          │
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│ 5. Execute workflow                 │
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│ 6. Aggregate results                │
└─────────────────────────────────────┘
                ↓
┌─────────────────────────────────────┐
│ 7. Deliver to user                  │
└─────────────────────────────────────┘
```

## Critical Rules

1. ✓ **ALWAYS activate orchestrator first** - Never skip this step
2. ✓ **EVERY task uses a skill** - No direct execution without skills
3. ✓ **Search before creating** - Use find-skills to check ecosystem
4. ✓ **Ask before installing** - Get user approval for new skills
5. ✓ **Let orchestrator decide patterns** - It optimizes execution
6. ✓ **Aggregate through orchestrator** - Ensures consistency

## Example Scenarios

### Simple Request
```
User: "Review this user story"
→ Orchestrator activates user-story-verifier
→ Results returned
```

### Missing Skill
```
User: "Create API tests with Postman"
→ Orchestrator checks inventory: No Postman skill
→ find-skills searches ecosystem
→ Presents options to user
→ User selects, skill installed
→ Orchestrator executes with new skill
```

### Complex Multi-Phase
```
User: "Review requirements and create E2E tests"
→ Orchestrator plans sequential workflow:
   Phase 1: user-story-verifier (analyze)
   Phase 2: (search for automation skill)
   Phase 3: (execute automation)
→ Aggregates results from all phases
→ Delivers comprehensive report
```

## Benefits of This Architecture

- **Modularity**: Each skill is self-contained and focused
- **Scalability**: Easy to add new skills for new capabilities
- **Maintainability**: Small, focused skills vs one giant file
- **Discoverability**: Skills can be found and shared
- **Reusability**: Skills can be used across projects
- **Consistency**: Orchestrator ensures uniform execution
- **Flexibility**: System adapts to missing capabilities

## Skills Directory Structure

```
.agents/skills/
├── browser-use/
├── cicd-testing-integration/
├── defect-lifecycle-manager/
├── find-skills/
├── multi-agent-orchestration/
├── qa-process-improvement/
├── skill-creator/
├── test-design-istqb/
├── test-execution-manager/
└── user-story-verifier/
```

## Getting Started

1. Review the main `SKILL.md` to understand the Senior QA Engineer role
2. Explore individual skills in `.agents/skills/` directory
3. When making requests, let the orchestrator guide the workflow
4. Install additional skills as needed using `npx skills add`

## Quality Standards

All tasks ensure:
- ✓ Orchestrator-driven execution
- ✓ Skill-backed operations
- ✓ Requirements are testable
- ✓ Test cases have clear steps and expected results
- ✓ Defects include reproduction steps
- ✓ Automation follows best practices
- ✓ Coverage includes positive, negative, and edge cases
- ✓ Traceability from requirements to tests to defects
- ✓ Metrics drive continuous improvement

## Contributing

To add a new skill:
1. Use the **skill-creator** skill to generate structure
2. Place in `.agents/skills/[skill-name]/`
3. Follow SKILL.md template
4. Update this README
5. Test through orchestrator

## License

[Include license information]
