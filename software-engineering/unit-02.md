# Unit II: Requirement Elicitation, Analysis, and Specification

## 0. Syllabus
Functional and Non-functional requirements, Requirement Sources and Elicitation Techniques, Analysis Modeling for Function-oriented and Object-oriented software development, Use case Modeling, System and Software Requirement Specifications, Requirement Validation, Traceability

## 1. Types of Requirements

### 1.1 Functional Requirements
- Define what the system should do
- Describe system services, tasks, or functions
- Example: "The system shall allow users to log in using a username and password."

### 1.2 Non-Functional Requirements
- Define system qualities or constraints
- Specify how the system performs its functions
- Types:
  - **Performance** (speed, response time)
  - **Security** (data protection, access control)
  - **Usability** (ease of use)
  - **Reliability** (uptime, error rates)
  - **Maintainability** (ease of updates)
  - **Portability** (runs on different platforms)
- Example: "The system shall respond to user queries within 2 seconds."

```
┌─────────────────────────────────────────────────────────────┐
│                  REQUIREMENTS TYPES                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌──────────────┐      ┌────────────────────┐               │
│  │  Functional  │      │  Non-Functional    │               │
│  │ (What system │      │ (How system works) │               │
│  │   does)      │      │ (Quality, limits)  │               │
│  └──────────────┘      └────────────────────┘               │
└─────────────────────────────────────────────────────────────┘
```

## 2. Requirement Sources
- **Stakeholders**: Users, customers, managers, developers
- **Documents**: Existing system docs, manuals
- **Business Environment**: Laws, standards, market trends
- **Domain Experts**: People with deep knowledge of the field

## 3. Requirement Elicitation Techniques

```
┌─────────────────────────────────────────────────────────────┐
│                REQUIREMENT ELICITATION                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ Interviews  │  │  Question-  │  │  Workshops  │         │
│  │             │  │  naires     │  │             │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │  Brain-     │  │  Observa-   │  │  Prototyping│         │
│  │  storming   │  │  tion       │  │             │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

- **Interviews**: One-on-one discussions with stakeholders
- **Questionnaires**: Written sets of questions for large groups
- **Workshops**: Group meetings for collaborative requirement gathering
- **Brainstorming**: Generating ideas in groups
- **Observation**: Watching users interact with current systems
- **Prototyping**: Building sample versions for feedback

## 4. Analysis Modeling

### 4.1 Function-Oriented Analysis Modeling
- Focuses on processes/functions performed by the system
- Uses Data Flow Diagrams (DFD), Entity-Relationship Diagrams (ERD)

#### Data Flow Diagram (DFD) Example
```
┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│   User      │───▶│  Login      │───▶│  System      │
└─────────────┘      └─────────────┘      └─────────────┘
```

### 4.2 Object-Oriented Analysis Modeling
- Focuses on objects (entities) and their interactions
- Uses Class Diagrams, Object Diagrams, Sequence Diagrams

#### Class Diagram Example
```
┌─────────────┐
│   User      │
├─────────────┤
│+username    │
│+password    │
├─────────────┤
│+login()     │
└─────────────┘
```

## 5. Use Case Modeling
- Describes system behavior from the user's perspective
- **Use Case**: A sequence of actions performed by the system for a user
- **Actor**: A user or another system interacting with the system

#### Use Case Diagram Example
```
┌─────────────┐        ┌─────────────┐
│   User      │──────▶│   Login     │
└─────────────┘        └─────────────┘
```

## 6. System and Software Requirement Specifications (SRS)
- **SRS**: A detailed document describing system requirements
- **Purpose**: Acts as a contract between client and developer
- **Contents:**
  - Introduction
  - Overall Description
  - Functional Requirements
  - Non-Functional Requirements
  - System Features
  - External Interfaces
  - Constraints
  - Quality Attributes

## 7. Requirement Validation
- Ensures requirements are correct, complete, and feasible
- **Techniques:**
  - Reviews/Inspections
  - Prototyping
  - Test Case Generation
  - Checklists
- **Goals:**
  - No ambiguity
  - No contradictions
  - All requirements testable

## 8. Requirement Traceability
- Ability to track each requirement throughout the project lifecycle
- **Types:**
  - **Forward Traceability**: From requirements to design/code/test
  - **Backward Traceability**: From design/code/test back to requirements
- **Benefits:**
  - Ensures all requirements are implemented
  - Helps manage changes

```
┌─────────────────────────────────────────────────────────────┐
│                  REQUIREMENT TRACEABILITY                   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Requirements → Design → Implementation → Testing           │
│         ▲                                         │         │
│         └─────────────────────────────────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

---

## Quick Revision Points

- **Functional vs Non-Functional**: What vs How
- **Elicitation Techniques**: Interviews, Questionnaires, Workshops, Brainstorming, Observation, Prototyping
- **Analysis Modeling**: Function-oriented (DFD, ERD), Object-oriented (Class, Sequence Diagrams)
- **Use Case**: User-system interaction
- **SRS**: Contract, detailed requirements
- **Validation**: Reviews, prototyping, test cases
- **Traceability**: Track requirements through project