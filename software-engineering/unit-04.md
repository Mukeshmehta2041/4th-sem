# Unit IV: Software Analysis and Testing

## 0. Syllabus
Software Static and Dynamic analysis, Code inspections, Software Testing Fundamentals, Software Test Process, Testing Levels, Test Criteria, Test Case Design, Test Oracles, Test Techniques, Black-Box Testing, White-Box Unit Testing and Unit Testing Frameworks, Integration Testing, System Testing and other Specialized Testing, Test Plan, Test Metrics, Testing Tools, Introduction to Object-oriented analysis, design and comparison with structured Software Engineering

## 1. Software Static and Dynamic Analysis
- **Static Analysis**: Examining code without executing it
  - Tools: Linters, static analyzers
  - Detects: Syntax errors, code smells, security issues
- **Dynamic Analysis**: Examining software during execution
  - Tools: Profilers, debuggers
  - Detects: Runtime errors, memory leaks, performance issues

```
┌─────────────────────────────────────────────────────────────┐
│           STATIC vs DYNAMIC ANALYSIS                        │
├─────────────────────────────────────────────────────────────┤
│  Static: No execution, code review, early detection         │
│  Dynamic: During execution, runtime issues                  │
└─────────────────────────────────────────────────────────────┘
```

## 2. Code Inspections
- **Definition**: Manual examination of code by peers
- **Purpose**: Find defects early, improve code quality
- **Types**: Walkthroughs, reviews, inspections
- **Benefits**: Early bug detection, knowledge sharing

## 3. Software Testing Fundamentals
- **Goal**: Ensure software meets requirements and is defect-free
- **Principles**:
  - Testing shows presence of defects
  - Exhaustive testing is impossible
  - Early testing saves time and cost
  - Defect clustering
  - Pesticide paradox (tests need to be updated)

## 4. Software Test Process
- **Phases**:
  1. Test Planning
  2. Test Design
  3. Test Execution
  4. Defect Reporting
  5. Test Closure

```
┌─────────────────────────────────────────────────────────────┐
│                  SOFTWARE TEST PROCESS                      │
├─────────────────────────────────────────────────────────────┤
│  Planning → Design → Execution → Reporting → Closure        │
└─────────────────────────────────────────────────────────────┘
```

## 5. Testing Levels
- **Unit Testing**: Test individual components
- **Integration Testing**: Test combined components
- **System Testing**: Test complete system
- **Acceptance Testing**: Test with user requirements
- **Specialized Testing**: Security, performance, usability, etc.

## 6. Test Criteria
- **Test Coverage**: Percentage of code/requirements tested
- **Pass/Fail Criteria**: Define when a test is successful
- **Entry/Exit Criteria**: Conditions to start/stop testing

## 7. Test Case Design
- **Test Case**: Set of inputs, execution conditions, and expected results
- **Design Techniques**:
  - Equivalence Partitioning
  - Boundary Value Analysis
  - Decision Table Testing
  - State Transition Testing

## 8. Test Oracles
- **Definition**: Mechanism to determine if test passed or failed
- **Types**: Specified output, heuristic, human judgment

## 9. Test Techniques
- **Black-Box Testing**: Test without knowledge of internal code
  - Focus: Inputs/outputs, requirements
  - Examples: Functional, system, acceptance testing
- **White-Box Testing**: Test with knowledge of internal code
  - Focus: Code structure, logic paths
  - Examples: Unit testing, code coverage

```
┌─────────────────────────────────────────────────────────────┐
│                TESTING TECHNIQUES                           │
├─────────────────────────────────────────────────────────────┤
│  Black-Box: Requirements-based, no code knowledge           │
│  White-Box: Code-based, logic paths, coverage               │
└─────────────────────────────────────────────────────────────┘
```

## 10. Unit Testing and Unit Testing Frameworks
- **Unit Testing**: Testing smallest testable parts (functions, methods)
- **Frameworks**: JUnit (Java), PyTest (Python), NUnit (.NET)
- **Benefits**: Early bug detection, easier refactoring

## 11. Integration Testing
- **Purpose**: Test interactions between integrated units/modules
- **Approaches**:
  - Top-down
  - Bottom-up
  - Big bang
  - Incremental

## 12. System Testing and Specialized Testing
- **System Testing**: Test complete, integrated system
- **Specialized Testing**:
  - Security Testing
  - Performance Testing
  - Usability Testing
  - Compatibility Testing

## 13. Test Plan
- **Definition**: Document describing scope, approach, resources, and schedule of testing
- **Contents**:
  - Test objectives
  - Test items
  - Features to be tested
  - Test deliverables
  - Schedule

## 14. Test Metrics
- **Purpose**: Measure effectiveness and quality of testing
- **Examples**:
  - Defect density
  - Test coverage
  - Test execution rate
  - Defect removal efficiency

## 15. Testing Tools
- **Static Analysis Tools**: SonarQube, ESLint
- **Test Management Tools**: TestRail, Zephyr
- **Automation Tools**: Selenium, JUnit, PyTest
- **Performance Tools**: JMeter, LoadRunner

## 16. Introduction to Object-Oriented Analysis and Design (OOAD)
- **OOAD**: Approach focusing on objects, classes, and their interactions
- **Key Concepts**:
  - Encapsulation
  - Inheritance
  - Polymorphism
  - Abstraction
- **Benefits**:
  - Reusability
  - Modularity
  - Easier maintenance

## 17. Comparison: OOAD vs Structured Software Engineering

| Aspect         | OOAD                        | Structured SE                |
|---------------|-----------------------------|------------------------------|
| Focus         | Objects & classes           | Functions & processes        |
| Modeling      | UML diagrams                | DFDs, ER diagrams            |
| Reusability   | High                        | Low                          |
| Modularity    | Object-based                | Function-based               |
| Change Mgmt   | Easier                      | Harder                       |

---

## Quick Revision Points: Analysis and Testing

- **Static vs Dynamic Analysis**: Code review vs runtime analysis
- **Testing Levels**: Unit, Integration, System, Acceptance
- **Test Techniques**: Black-box, White-box
- **Test Case Design**: Equivalence, Boundary, Decision Table
- **Test Plan**: Scope, objectives, schedule
- **Metrics**: Defect density, coverage
- **OOAD vs Structured**: Objects vs functions, UML vs DFD 