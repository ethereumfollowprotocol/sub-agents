# LLM Agent Development Specification

## Overview

This specification defines an organizational framework for Large Language Model (LLM) agent development that improves results through clear expectations, boundaries, and structured processes. The framework emphasizes immersive context creation, role separation, and iterative development cycles.

## Core Principles

### 1. Immersive Context Creation
Agents should create rich, detailed contexts that provide comprehensive understanding. Immersion is achieved through:
- **Shared Context**: All agents must maintain consistent understanding of the project state
- **Descriptive Language**: Use clear, vivid descriptions that establish context and expectations
- **Narrative Continuity**: Each interaction should build upon previous context

**Example**: Instead of "Fix the login bug," use "The authentication gateway is failing to properly validate user credentials, causing users to be locked out of their accounts. The validation mechanism appears to have degraded, possibly due to recent infrastructure changes. Investigate the credential validation process and restore proper system access."

### 2. Separation of Responsibilities
Agents are organized into distinct roles with specific responsibilities:

#### Goal Evaluation Agents
- **Purpose**: Assess high-level objectives and strategic direction
- **Responsibilities**: 
  - Analyze project goals for clarity and achievability
  - Identify potential conflicts or dependencies
  - Provide strategic recommendations
- **Context**: Strategic oversight role - maintains holistic view of organizational objectives

#### Task Generation Agents  
- **Purpose**: Transform goals into actionable tasks
- **Responsibilities**:
  - Create detailed Product Requirement Documents (PRDs)
  - Break down complex objectives into executable steps
  - Define success criteria and acceptance conditions
- **Context**: Requirements architect - transforms high-level goals into detailed implementation plans

#### Task Evaluation Agents
- **Purpose**: Assess individual task quality and completeness
- **Responsibilities**:
  - Review task specifications for clarity
  - Validate task feasibility and resource requirements
  - Ensure tasks align with broader goals
- **Context**: Quality assurance role - validates specifications meet standards and requirements

#### Execution Agents
- **Purpose**: Implement tasks and deliver results
- **Responsibilities**:
  - Execute assigned tasks according to specifications
  - Report progress and blockers
  - Deliver measurable outcomes
- **Context**: Implementation specialists - execute tasks according to specifications

## Development Cycle

The development process follows a structured cycle designed to maintain quality and alignment:

### Phase 1: Goal Evaluation
**Agent Type**: Goal Evaluation Agent
**Input**: Project requirements, organizational context
**Activities**:
- Review and clarify organizational objectives
- Assess current project state and context
- Identify success metrics and constraints
- Generate strategic recommendations

**Output**: `STRATEGY.md`

### Phase 2: Task Generation
**Agent Type**: Task Generation Agent
**Input**: `STRATEGY.md`
**Activities**:
- Transform goals into specific, actionable tasks
- Create detailed Product Requirement Documents for each task
- Define clear acceptance criteria and success metrics
- Establish task priorities and dependencies

**Output**: `TASKLIST.md`

**PRD Template**:
```
# Task: [Descriptive Name]

## Context
[Rich, detailed description of the current situation and environment]

## Objective
[Clear statement of what needs to be accomplished]

## Success Criteria
- [ ] Specific, measurable outcome 1
- [ ] Specific, measurable outcome 2
- [ ] Specific, measurable outcome 3

## Constraints
- Technical limitations
- Resource constraints
- Timeline requirements

## Examples
[Provide concrete examples of expected outputs]

## Dependencies
- Prerequisites that must be completed first
- Resources or information required
```

### Phase 3: Current Tasklist Evaluation
**Agent Type**: Task Evaluation Agent
**Input**: `TASKLIST.md`
**Activities**:
- Review generated tasks for quality and completeness
- Validate task specifications meet requirements
- Identify potential issues or improvements
- Prioritize tasks based on impact and dependencies

**Output**: `VALIDATED_TASKS.md`

### Phase 4: Begin Tasklist Execution
**Agent Type**: Execution Agent
**Input**: `VALIDATED_TASKS.md`
**Activities**:
- Execute tasks according to specifications
- Monitor progress and report status
- Handle new task creation as needed
- Address immediate blockers or issues

**Output**: `EXECUTION_PROGRESS.md` (continuously updated)

### Phase 4a: New Task Creation (During Execution)
When new tasks are identified during execution:

**Immediate Addressing**:
- If task is critical to current work: pause and address immediately
- Create mini-PRD for urgent task
- Execute and return to original task

**Backlog Addition**:
- If task is important but not urgent: add to backlog
- Include full context and reasoning
- Prioritize relative to existing backlog items

### Phase 5: Finish Task List
**Agent Type**: Execution Agent
**Input**: `EXECUTION_PROGRESS.md`
**Activities**:
- Complete all tasks in current sprint
- Validate deliverables against success criteria
- Document outcomes and lessons learned
- Prepare handoff materials

**Output**: `TASK_RESULTS.md`

### Phase 6: Backlog Evaluation
**Agent Type**: Task Evaluation Agent
**Input**: `TASK_RESULTS.md`, existing `BACKLOG.md`
**Activities**:
- Review accumulated backlog items
- Re-prioritize based on current context
- Identify obsolete or duplicate items
- Prepare recommendations for next cycle

**Output**: Updated `BACKLOG.md`

### Phase 7: Goal Evaluation (Cycle Completion)
**Agent Type**: Goal Evaluation Agent
**Input**: `TASK_RESULTS.md`, `BACKLOG.md`
**Activities**:
- Assess progress toward strategic objectives
- Identify lessons learned and process improvements
- Adjust goals based on new information
- Prepare for next development cycle

**Output**: Updated `STRATEGY.md` for next cycle

## Task Tracking System

### Repository-Level Task Management
Each repository implementing this specification must maintain a comprehensive task history using a standardized tracking system located in the repository root.

#### Directory Structure
```
.tasks/
├── TASK-001.md
├── TASK-002.md
├── TASK-003.md
└── ...
```

#### Task File Naming Convention
- **Format**: `TASK-###.md` where `###` is a zero-padded, incrementing counter
- **Counter**: Starts at 001 and increments for each new task in the repository
- **Scope**: Counter is repository-specific, not global across projects

#### Task File Structure
Each task file must contain the following sections:

```markdown
# TASK-### - [Task Title]

## Metadata
- **Created**: [ISO 8601 timestamp]
- **Status**: [pending|in_progress|completed|cancelled]
- **Agent**: [Agent type that handled this task]
- **Priority**: [high|medium|low]
- **Cycle**: [Development cycle identifier]

## Original PRD
[Complete Product Requirement Document as generated in Phase 2]

## Implementation Details
### Approach
[Description of the implementation strategy and methodology used]

### Changes Made
[Detailed list of all modifications, additions, or deletions]

### Technical Decisions
[Key architectural or implementation choices with rationale]

## Outcomes
### Deliverables
[List of concrete outputs produced]

### Success Metrics
- [ ] [Original success criterion 1] - [Status: ✅ Met / ❌ Not Met / 🔄 Partial]
- [ ] [Original success criterion 2] - [Status: ✅ Met / ❌ Not Met / 🔄 Partial]

### Lessons Learned
[Key insights and improvements for future tasks]

## References
### Issues
- [Issue #123: Description](link-to-issue)
- [Issue #456: Description](link-to-issue)

### Pull Requests
- [PR #789: Description](link-to-pr)
- [PR #101: Description](link-to-pr)

### Related Tasks
- [TASK-002: Related task title](.tasks/TASK-002.md)
- [TASK-005: Dependent task title](.tasks/TASK-005.md)

## Timeline
- **Started**: [ISO 8601 timestamp]
- **Completed**: [ISO 8601 timestamp]
- **Duration**: [Time spent on task]
```

#### Task Management Requirements

##### Task Creation
- Create task file immediately when execution begins (Phase 4)
- Populate metadata and original PRD sections
- Set status to `in_progress`
- Commit task file to repository

##### Progress Updates
- Update `Implementation Details` section as work progresses
- Document significant decisions and changes in real-time
- Link to issues and pull requests as they are created
- Maintain current status in metadata

##### Task Completion
- Complete all sections including outcomes and metrics
- Set status to `completed` or `cancelled`
- Add completion timestamp
- Ensure all references are properly linked
- Final commit with completed task file

##### Integration with Development Workflow
- Task files must be created before any implementation work begins
- All issues created during task execution must be referenced
- All pull requests must reference the relevant task file
- Task completion blocks should reference specific task files
- Code reviews should validate task file completeness

#### Task Discovery and Navigation
Repositories should maintain a `TASKS_INDEX.md` file in the `.tasks` directory that provides:
- Chronological list of all tasks
- Status summary dashboard
- Cross-references between related tasks
- Quick access to recently completed work

**Example TASKS_INDEX.md**:
```markdown
# Task Index

## Quick Stats
- Total Tasks: 15
- Completed: 12
- In Progress: 2
- Cancelled: 1

## Recent Tasks
| Task | Title | Status | Agent | Date |
|------|-------|--------|-------|------|
| [TASK-015](TASK-015.md) | Authentication Security Enhancement | ✅ Completed | Execution | 2024-01-15 |
| [TASK-014](TASK-014.md) | API Rate Limiting Implementation | 🔄 In Progress | Execution | 2024-01-12 |

## All Tasks
[Chronological listing of all tasks with links]
```

## Implementation Guidelines

### Context Management
- Maintain a shared context document that all agents can access
- Update context after each phase completion
- Include relevant examples and precedents
- Document decisions and rationale
- Reference relevant task files for historical context

### Communication Standards
- Use descriptive, immersive language in all communications
- Provide concrete examples whenever possible
- Maintain narrative consistency across agent interactions
- Document assumptions and clarifications
- Include task file references in all implementation discussions

### Quality Assurance
- Each phase must produce specified deliverables
- Validation checkpoints ensure quality standards
- Regular retrospectives improve the process
- Metrics track effectiveness and efficiency
- Task completion requires fully documented task files

## Example Implementation

### Scenario: Improving User Authentication System

**Goal Evaluation Phase**:
"The organization's authentication infrastructure has shown degradation in security posture, with potential vulnerabilities that could allow unauthorized access to critical systems. We need to strengthen these security mechanisms while maintaining seamless user experience for legitimate users."

**Task Generation Phase**:
```
# Task: Strengthen Authentication Security Mechanisms

## Context
The current authentication system has shown vulnerabilities in recent security assessments. Users report slow login times, and security monitoring has detected unauthorized access attempts targeting the authentication endpoints.

## Objective  
Implement multi-factor authentication and improve login performance while maintaining security standards.

## Success Criteria
- [ ] Multi-factor authentication implemented for all user types
- [ ] Login performance improved by 40% from current baseline
- [ ] Zero security vulnerabilities in penetration testing
- [ ] 95% user satisfaction in usability testing

## Examples
- SMS-based second factor for standard users
- Hardware token support for administrative roles
- Biometric options for high-security access
```

## Document Definitions

### STRATEGY.md
**Purpose**: Strategic assessment and high-level planning document
**Properties**:
- **Objectives**: Clear statement of organizational goals
- **Current State**: Assessment of existing systems and capabilities
- **Success Metrics**: Quantifiable measures of goal achievement
- **Constraints**: Resource, technical, and timeline limitations
- **Risk Assessment**: Potential issues and mitigation strategies
- **Strategic Recommendations**: High-level approach and priorities

### TASKLIST.md
**Purpose**: Detailed task specifications with implementation requirements
**Properties**:
- **Task Inventory**: Complete list of tasks with unique identifiers
- **Task PRDs**: Individual Product Requirement Documents for each task
- **Dependencies**: Inter-task relationships and prerequisites
- **Priority Matrix**: Task prioritization with justification
- **Resource Requirements**: Skills, tools, and time estimates needed
- **Timeline**: Proposed sequence and scheduling

### VALIDATED_TASKS.md
**Purpose**: Quality-assured task specifications ready for execution
**Properties**:
- **Approved Tasks**: Tasks that passed validation criteria
- **Validation Notes**: Quality assessment findings for each task
- **Risk Mitigation**: Identified risks and proposed solutions
- **Execution Order**: Optimized sequence based on dependencies
- **Resource Allocation**: Confirmed availability of required resources
- **Acceptance Criteria**: Final validation requirements for each task

### EXECUTION_PROGRESS.md
**Purpose**: Real-time tracking of task execution status
**Properties**:
- **Task Status**: Current state (not started, in progress, completed, blocked)
- **Progress Updates**: Timestamped status changes and notes
- **Blockers**: Issues preventing task completion with escalation paths
- **Deliverables**: Completed outputs and artifacts
- **Time Tracking**: Actual vs. estimated effort
- **Quality Metrics**: Performance indicators during execution

### TASK_RESULTS.md
**Purpose**: Comprehensive summary of completed work and outcomes
**Properties**:
- **Completion Summary**: Final status of all tasks in the cycle
- **Deliverables Catalog**: All outputs produced with quality validation
- **Lessons Learned**: Key insights and improvement recommendations
- **Performance Metrics**: Actual vs. planned time, quality, and scope
- **Outstanding Issues**: Unresolved items requiring future attention
- **Handoff Documentation**: Information needed for subsequent phases

### BACKLOG.md
**Purpose**: Prioritized inventory of future work items
**Properties**:
- **Backlog Items**: Tasks not included in current cycle with descriptions
- **Priority Ranking**: Ordered list with business value assessment
- **Effort Estimates**: High-level sizing for planning purposes
- **Context Preservation**: Background information for future reference
- **Stakeholder Input**: Requirements and feedback from various parties
- **Cycle Recommendations**: Suggestions for future sprint planning

This specification provides the framework for consistent, high-quality LLM agent development while maintaining the immersive, context-rich approach that leads to better outcomes.