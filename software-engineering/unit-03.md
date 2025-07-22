# Unit III: Software Design

## 0. Syllabus
Software Design The Software Design Process, Design Concepts and Principles, Software Modeling and UML, Architectural Design, Architectural Views and Styles, User Interface Design, Function-oriented Design, SA/SD, Component Based Design, Design Metrics

## 1. The Software Design Process

- **Definition**: The process of defining the architecture, components, interfaces, and other characteristics of a system or component.
- **Goal**: Transform requirements into a blueprint for constructing the software.

### Design Process Steps
```
┌─────────────────────────────────────────────────────────────┐
│                SOFTWARE DESIGN PROCESS                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. Requirement Analysis                                    │
│  2. System/Architectural Design                            │
│  3. Detailed Design                                        │
│  4. Implementation                                         │
│  5. Testing                                                │
└─────────────────────────────────────────────────────────────┘
```
- **System Design**: Defines overall system architecture
- **Detailed Design**: Specifies internal logic of components

## 2. Design Concepts and Principles

### Key Concepts
- **Abstraction**: Focusing on essential qualities, ignoring details
- **Refinement**: Gradually elaborating details
- **Modularity**: Dividing system into manageable parts
- **Information Hiding**: Concealing internal details
- **Cohesion**: Degree to which elements of a module belong together
- **Coupling**: Degree of interdependence between modules
- **Separation of Concerns**: Dividing complex problems into distinct features

### Principles
- **Single Responsibility Principle**: Each module has one responsibility
- **Open/Closed Principle**: Open for extension, closed for modification
- **DRY (Don't Repeat Yourself)**: Avoid duplication
- **KISS (Keep It Simple, Stupid)**: Simplicity is key

## 3. Software Modeling and UML

- **Modeling**: Creating abstract representations of the system
- **UML (Unified Modeling Language)**: Standard for visualizing, specifying, constructing, and documenting software systems

### Common UML Diagrams
```
┌─────────────────────────────────────────────────────────────┐
│                        UML DIAGRAMS                         │
├─────────────────────────────────────────────────────────────┤
│  • Use Case Diagram                                         │
│  • Class Diagram                                            │
│  • Sequence Diagram                                         │
│  • Activity Diagram                                         │
│  • State Diagram                                            │
│  • Component Diagram                                        │
│  • Deployment Diagram                                       │
└─────────────────────────────────────────────────────────────┘
```
- **Use Case Diagram**: User interactions
- **Class Diagram**: System structure
- **Sequence Diagram**: Object interactions over time
- **Activity Diagram**: Workflow
- **State Diagram**: State changes
- **Component Diagram**: Software components
- **Deployment Diagram**: Physical deployment

## 4. Architectural Design

- **Definition**: High-level structuring of software system
- **Purpose**: Define major components and their interactions

### Architectural Design Activities
- **Defining Subsystems**
- **Specifying Interfaces**
- **Establishing Relationships**

### Common Architectural Styles
```
┌─────────────────────────────────────────────────────────────┐
│                  ARCHITECTURAL STYLES                       │
├─────────────────────────────────────────────────────────────┤
│  • Layered Architecture                                     │
│  • Client-Server                                           │
│  • Pipe-and-Filter                                         │
│  • Event-Driven                                            │
│  • Microservices                                           │
└─────────────────────────────────────────────────────────────┘
```

## 5. Architectural Views and Styles

- **Architectural Views**: Different perspectives of the system architecture
  - **Logical View**: Functionality
  - **Process View**: Concurrency, processes
  - **Development View**: Software organization
  - **Physical View**: Deployment
- **Styles**: Patterns for organizing system structure (see above)

## 6. User Interface Design

- **Goal**: Make system easy and efficient for users
- **Principles**:
  - Consistency
  - Feedback
  - Simplicity
  - Error Prevention
  - User Control

### UI Design Process
- **Understand Users**
- **Design Prototypes**
- **Evaluate and Refine**

## 7. Function-Oriented Design

- **Focus**: Functions performed by the system
- **Tools**: Data Flow Diagrams (DFD), Structure Charts

### SA/SD (Structured Analysis/Structured Design)
- **SA**: Analyzes system using DFDs
- **SD**: Converts DFDs into structure charts for design

```
┌─────────────────────────────────────────────────────────────┐
│                  FUNCTION-ORIENTED DESIGN                   │
├─────────────────────────────────────────────────────────────┤
│  • Data Flow Diagrams (DFD)                                 │
│  • Structure Charts                                         │
└─────────────────────────────────────────────────────────────┘
```

## 8. Component-Based Design

- **Definition**: Building software from pre-existing components
- **Advantages**:
  - Reusability
  - Faster development
  - Easier maintenance
- **Process**:
  1. Identify required components
  2. Select or develop components
  3. Integrate components

## 9. Design Metrics

- **Purpose**: Quantitative measures to assess design quality

### Common Metrics
- **Coupling**: Degree of interdependence between modules
- **Cohesion**: Degree to which elements of a module belong together
- **Fan-in/Fan-out**: Number of modules calling/called by a module
- **Size Metrics**: Number of classes, methods, etc.
- **Complexity Metrics**: Cyclomatic complexity

---

## Quick Revision Points

### Design Concepts
```
┌─────────────────────────────────────────────────────────────┐
│                    DESIGN CONCEPTS                          │
├─────────────────────────────────────────────────────────────┤
│  Abstraction, Modularity, Information Hiding, Cohesion,     │
│  Coupling, Separation of Concerns                           │
└─────────────────────────────────────────────────────────────┘
```

### UML Diagrams
- Use Case, Class, Sequence, Activity, State, Component, Deployment

### Architectural Styles
- Layered, Client-Server, Pipe-and-Filter, Event-Driven, Microservices

### UI Design Principles
- Consistency, Feedback, Simplicity, Error Prevention, User Control

### Function-Oriented Design
- DFD, Structure Charts, SA/SD

### Component-Based Design
- Reusability, Integration

### Design Metrics
- Coupling, Cohesion, Fan-in/Fan-out, Size, Complexity 