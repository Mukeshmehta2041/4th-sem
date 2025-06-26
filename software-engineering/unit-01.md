# Unit I: The Software Product and Software Process

## 0. Syllabus
The Software Product and Software Process Software Product and Process Characteristics, Software Process Models: LinearSequential Model, Prototyping Model, RAD Model, Evolutionary Process Models likeIncremental Model, Spiral Model, Component Assembly Model, RUP and Agileprocesses. Software Process customization and improvement, CMM, Product andProcess Metrics

## 1. Software Product and Process Characteristics

### Software Product Characteristics
```
┌─────────────────────────────────────────────────────────────┐
│                    SOFTWARE PRODUCT                         │
├─────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ Intangible  │  │   Complex   │  │  Flexible   │         │
│  │   (No physical │  │(Many inter- │  │(Easily modi-│         │
│  │    form)    │  │  related    │  │   fiable)   │         │
│  │             │  │ components) │  │             │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Durable   │  │  Reliable   │  │Maintainable │         │
│  │(No physical │  │(Consistent  │  │(Easy to mod-│         │
│  │   wear)     │  │performance) │  │   ify)      │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐                          │
│  │  Portable   │  │  Reusable   │                          │
│  │(Runs on dif-│  │(Components  │                          │
│  │ferent plat- │  │can be reused│                          │
│  │   forms)    │  │in projects) │                          │
│  └─────────────┘  └─────────────┘                          │
└─────────────────────────────────────────────────────────────┘
```

- **Intangible**: Cannot be seen, touched, or physically measured
- **Complex**: Contains many interrelated components
- **Flexible**: Can be easily modified and adapted
- **Durable**: Does not wear out physically
- **Reliable**: Must perform consistently under various conditions
- **Maintainable**: Should be easy to modify and update
- **Portable**: Can run on different platforms
- **Reusable**: Components can be used in other projects

### Software Process Characteristics
```
┌─────────────────────────────────────────────────────────────┐
│                   SOFTWARE PROCESS                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ Systematic  │  │ Repeatable  │  │ Measurable  │         │
│  │(Follows de- │  │(Consistent  │  │(Quantifiable│         │
│  │ fined steps)│  │application) │  │  progress)  │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ Predictable │  │Controllable │  │ Improvable  │         │
│  │(Estimatable │  │(Monitorable │  │(Enhanceable │         │
│  │  outcomes)  │  │& adjustable)│  │  processes) │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
└─────────────────────────────────────────────────────────────┘
```

- **Systematic**: Follows defined steps and procedures
- **Repeatable**: Can be applied consistently across projects
- **Measurable**: Progress and quality can be quantified
- **Predictable**: Outcomes can be estimated with reasonable accuracy
- **Controllable**: Can be monitored and adjusted as needed
- **Improvable**: Can be enhanced based on experience and feedback

## 2. Software Process Models

### 2.1 Linear Sequential Model (Waterfall Model)
```
┌─────────────────────────────────────────────────────────────┐
│                    WATERFALL MODEL                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │Requirements │───▶│   System    │───▶│Implementation│     │
│  │  Analysis   │    │   Design    │    │             │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Testing   │◀───│Deployment   │◀───│ Maintenance │     │
│  │             │    │             │    │             │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Each phase must be completed before moving to the next     │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Sequential, linear approach
- Each phase must be completed before moving to the next
- Clear milestones and deliverables

**Phases:**
1. **Requirements Analysis** → System requirements specification
2. **System Design** → Software architecture and design documents
3. **Implementation** → Code development
4. **Testing** → Verification and validation
5. **Deployment** → Installation and delivery
6. **Maintenance** → Updates and bug fixes

**Advantages:**
- Simple and easy to understand
- Clear documentation at each stage
- Good for well-defined, stable requirements

**Disadvantages:**
- Inflexible to changes
- Late feedback on product quality
- High risk of project failure
- Not suitable for complex or evolving requirements

### 2.2 Prototyping Model
```
┌─────────────────────────────────────────────────────────────┐
│                   PROTOTYPING MODEL                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │Requirements │───▶│  Quick      │───▶│ Prototype   │     │
│  │ Gathering   │    │  Design     │    │Development  │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         ▲                   │                   │           │
│         │                   ▼                   ▼           │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ Refinement  │◀───│   User      │◀───│   Final     │     │
│  │             │    │ Evaluation  │    │  Product    │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Iterative feedback loop with user involvement              │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Builds working prototypes to understand requirements
- Iterative approach with user feedback
- Reduces risk of misunderstanding requirements

**Process:**
1. **Requirements Gathering** → Initial requirements collection
2. **Quick Design** → Rapid prototype design
3. **Prototype Development** → Build working prototype
4. **User Evaluation** → Get feedback from users
5. **Refinement** → Improve prototype based on feedback
6. **Final Product** → Develop complete system

**Advantages:**
- Early user involvement
- Reduces requirement ambiguity
- Faster feedback cycle
- Better user satisfaction

**Disadvantages:**
- May lead to incomplete analysis
- Users may focus on prototype rather than requirements
- Can be time-consuming if over-iterated

### 2.3 RAD Model (Rapid Application Development)
```
┌─────────────────────────────────────────────────────────────┐
│                        RAD MODEL                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │  Business   │───▶│    Data     │───▶│   Process   │     │
│  │ Modeling    │    │  Modeling   │    │  Modeling   │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────┐    ┌─────────────┐                        │
│  │Application  │───▶│ Testing &   │                        │
│  │ Generation  │    │ Turnover    │                        │
│  │(Automated   │    │             │                        │
│  │   tools)    │    │             │                        │
│  └─────────────┘    └─────────────┘                        │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Fast development with parallel teams and reusable components│
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Fast development with minimal planning
- Uses reusable components
- Parallel development teams
- Time-boxed iterations

**Phases:**
1. **Business Modeling** → Define business processes
2. **Data Modeling** → Design database structure
3. **Process Modeling** → Define application processes
4. **Application Generation** → Build using automated tools
5. **Testing & Turnover** → Test and deploy

**Advantages:**
- Very fast development
- High user involvement
- Reusable components
- Reduced development time

**Disadvantages:**
- Requires highly skilled developers
- Not suitable for large, complex projects
- Heavy dependency on modeling skills
- Limited scalability

### 2.4 Evolutionary Process Models

#### 2.4.1 Incremental Model
```
┌─────────────────────────────────────────────────────────────┐
│                   INCREMENTAL MODEL                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ Increment 1 │───▶│ Increment 2 │───▶│ Increment 3 │     │
│  │(Core func-  │    │(Additional  │    │(More        │     │
│  │ tionality)  │    │ features)   │    │ features)   │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Deliver   │    │   Deliver   │    │   Deliver   │     │
│  │   to User   │    │   to User   │    │   to User   │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Each increment adds functionality and can be delivered     │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Divides software into small, manageable increments
- Each increment adds functionality
- Can be delivered to users after each increment

**Process:**
1. **Increment 1** → Core functionality
2. **Increment 2** → Additional features
3. **Increment 3** → More features
4. **...** → Continue until complete

**Advantages:**
- Early delivery of working software
- Reduced risk
- Easy to test and validate
- User feedback at each stage

**Disadvantages:**
- Requires good planning
- May lead to integration issues
- Can be expensive if not planned well

#### 2.4.2 Spiral Model
```
┌─────────────────────────────────────────────────────────────┐
│                     SPIRAL MODEL                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                    ┌─────────────┐                         │
│                   │   Planning   │                         │
│                    └─────────────┘                         │
│                           │                                │
│                           ▼                                │
│                    ┌─────────────┐                         │
│                   │ Risk Analysis│                         │
│                    └─────────────┘                         │
│                           │                                │
│                           ▼                                │
│                    ┌─────────────┐                         │
│                   │ Engineering  │                         │
│                    └─────────────┘                         │
│                           │                                │
│                           ▼                                │
│                    ┌─────────────┐                         │
│                   │ Evaluation   │                         │
│                    └─────────────┘                         │
│                           │                                │
│                           ▼                                │
│                    ┌─────────────┐                         │
│                   │   Planning   │                         │
│                    └─────────────┘                         │
│                           │                                │
│                           ▼                                │
│                    ┌─────────────┐                         │
│                   │ Risk Analysis│                         │
│                    └─────────────┘                         │
│                                                            │
│  ════════════════════════════════════════════════════════  │
│  Each spiral cycle includes risk analysis and evaluation   │
└────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Combines iterative development with systematic risk management
- Each iteration is a complete development cycle
- Risk analysis at each phase

**Spiral Cycles:**
1. **Planning** → Define objectives and constraints
2. **Risk Analysis** → Identify and analyze risks
3. **Engineering** → Develop and test
4. **Evaluation** → Review and plan next iteration

**Advantages:**
- Excellent risk management
- Flexible and adaptable
- Early risk identification
- Suitable for large, complex projects

**Disadvantages:**
- Complex to implement
- Requires expertise in risk analysis
- Can be expensive
- Difficult to manage

#### 2.4.3 Component Assembly Model
```
┌─────────────────────────────────────────────────────────────┐
│                COMPONENT ASSEMBLY MODEL                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │ Component   │───▶│ Component   │───▶│ Component   │     │
│  │ Analysis    │    │ Selection   │    │ Adaptation  │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────┐    ┌─────────────┐                        │
│  │ Component   │───▶│   System    │                        │
│  │Integration  │    │  Testing    │                        │
│  │             │    │             │                        │
│  └─────────────┘    └─────────────┘                        │
│                                                            │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │   Pre-built │  │   Pre-built │  │   Pre-built │         │
│  │ Components  │  │ Components  │  │ Components  │         │
│  │             │  │             │  │             │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Uses existing, tested components for faster development    │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Uses pre-built, reusable components
- Focuses on component integration
- Reduces development time significantly

**Process:**
1. **Component Analysis** → Identify required components
2. **Component Selection** → Choose appropriate components
3. **Component Adaptation** → Modify components if needed
4. **Component Integration** → Assemble components
5. **System Testing** → Test integrated system

**Advantages:**
- Faster development
- Reduced cost
- Higher quality (tested components)
- Reusability

**Disadvantages:**
- Dependency on component availability
- Integration challenges
- Limited customization
- Quality depends on component quality

### 2.5 RUP (Rational Unified Process)
```
┌─────────────────────────────────────────────────────────────┐
│                        RUP MODEL                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │  Inception  │───▶│ Elaboration │───▶│Construction │     │
│  │(Scope &     │    │(Architecture│    │(Development)│     │
│  │ feasibility)│    │ & planning) │    │             │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────┐                                        │
│  │ Transition  │                                        │
│  │(Deployment  │                                        │
│  │ & training) │                                        │
│  └─────────────┘                                        │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │ Business    │  │Requirements │  │Analysis &   │         │
│  │ Modeling    │  │             │  │Design       │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐         │
│  │Implementation│  │    Test     │  │Deployment   │         │
│  └─────────────┘  └─────────────┘  └─────────────┘         │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  4 phases with 9 workflows running in parallel              │
└─────────────────────────────────────────────────────────────┘
```

**Characteristics:**
- Iterative and incremental approach
- Architecture-centric
- Risk-driven
- Use-case driven

**Phases:**
1. **Inception** → Project scope and feasibility
2. **Elaboration** → Architecture and detailed planning
3. **Construction** → System development
4. **Transition** → Deployment and user training

**Workflows:**
- Business Modeling
- Requirements
- Analysis & Design
- Implementation
- Test
- Deployment
- Configuration & Change Management
- Project Management
- Environment

**Advantages:**
- Comprehensive framework
- Good documentation
- Risk management
- Quality focus

**Disadvantages:**
- Complex to implement
- Requires training
- Can be bureaucratic
- Expensive

### 2.6 Agile Processes
```
┌─────────────────────────────────────────────────────────────┐
│                      AGILE PROCESSES                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    AGILE VALUES                         │ │
│  │                                                         │ │
│  │  Individuals & Interactions > Processes & Tools         │ │
│  │  Working Software > Comprehensive Documentation         │ │
│  │  Customer Collaboration > Contract Negotiation         │ │
│  │  Responding to Change > Following a Plan               │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │    Scrum    │    │      XP     │    │   Kanban    │     │
│  │             │    │             │    │             │     │
│  │ • Sprints   │    │ • Pair      │    │ • Visual    │     │
│  │ • Roles     │    │   Programming│    │   Board     │     │
│  │ • Ceremonies│    │ • TDD       │    │   Limits    │     │
│  │ • Artifacts │    │ • CI/CD     │    │   Limits    │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
│  ════════════════════════════════════════════════════════   │
│  Flexible, iterative approach with customer focus          │
└─────────────────────────────────────────────────────────────┘
```

**Core Principles:**
- Individuals and interactions over processes and tools
- Working software over comprehensive documentation
- Customer collaboration over contract negotiation
- Responding to change over following a plan

**Popular Agile Methods:**

#### Scrum
```
┌─────────────────────────────────────────────────────────────┐
│                         SCRUM                               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Sprint    │───▶│   Sprint    │───▶│   Sprint    │     │
│  │ Planning    │    │ Planning    │    │ Planning    │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Sprint    │    │   Sprint    │    │   Sprint    │     │
│  │ (2-4 weeks) │    │ (2-4 weeks) │    │ (2-4 weeks) │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Sprint    │    │   Sprint    │    │   Sprint    │     │
│  │  Review     │    │  Review     │    │  Review     │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
│  Roles: Product Owner, Scrum Master, Development Team      │
│  Ceremonies: Planning, Daily Standup, Review, Retrospective│
│  Artifacts: Product Backlog, Sprint Backlog, Increment     │
└─────────────────────────────────────────────────────────────┘
```

- **Sprint**: 2-4 week development cycles
- **Roles**: Product Owner, Scrum Master, Development Team
- **Ceremonies**: Sprint Planning, Daily Standup, Sprint Review, Sprint Retrospective
- **Artifacts**: Product Backlog, Sprint Backlog, Increment

#### Extreme Programming (XP)
- **Values**: Communication, Simplicity, Feedback, Courage
- **Practices**: Pair Programming, Test-Driven Development, Continuous Integration, Refactoring

#### Kanban
- **Visual board** with columns: To Do, In Progress, Done
- **Work in Progress (WIP)** limits
- **Continuous flow** of work items

**Advantages:**
- Fast delivery
- High customer satisfaction
- Adaptable to changes
- Better team collaboration

**Disadvantages:**
- Requires cultural change
- May lack documentation
- Difficult to predict timelines
- Requires experienced team

## 3. Software Process Customization and Improvement

### Process Customization
```
┌─────────────────────────────────────────────────────────────┐
│                PROCESS CUSTOMIZATION                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │  Standard   │───▶│  Tailoring  │───▶│  Customized │     │
│  │  Process    │    │             │    │  Process    │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│                                                             │
│  Factors: Project size, complexity, team experience, domain│
│  Benefits: Better fit, improved efficiency, reduced overhead│
└─────────────────────────────────────────────────────────────┘
```

- **Tailoring**: Adapting standard processes to project needs
- **Factors**: Project size, complexity, team experience, domain
- **Benefits**: Better fit, improved efficiency, reduced overhead

### Process Improvement
- **Continuous Improvement**: Ongoing enhancement of processes
- **Metrics**: Quantitative measures of process performance
- **Feedback Loops**: Learning from project experiences

## 4. CMM (Capability Maturity Model)
```
┌─────────────────────────────────────────────────────────────┐
│                    CMM LEVELS                               │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    LEVEL 5                              │ │
│  │                OPTIMIZING                               │ │
│  │           Continuous Process Improvement                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           ▲                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    LEVEL 4                              │ │
│  │                  MANAGED                                │ │
│  │           Quantitative Process Management               │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           ▲                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    LEVEL 3                              │ │
│  │                   DEFINED                               │ │
│  │        Standardized Processes Across Organization      │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           ▲                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    LEVEL 2                              │ │
│  │                 REPEATABLE                              │ │
│  │              Basic Project Management                   │ │
│  └─────────────────────────────────────────────────────────┘ │
│                           ▲                                │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                    LEVEL 1                              │ │
│  │                   INITIAL                               │ │
│  │              Chaotic, Unpredictable Processes           │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### CMM Levels:
1. **Initial (Level 1)**: Chaotic, unpredictable processes
2. **Repeatable (Level 2)**: Basic project management
3. **Defined (Level 3)**: Standardized processes across organization
4. **Managed (Level 4)**: Quantitative process management
5. **Optimizing (Level 5)**: Continuous process improvement

### Key Process Areas (KPAs):
- **Level 2**: Requirements Management, Project Planning, Project Tracking
- **Level 3**: Organization Process Focus, Training Program, Integrated Software Management
- **Level 4**: Quantitative Process Management, Software Quality Management
- **Level 5**: Defect Prevention, Technology Change Management, Process Change Management

## 5. Product and Process Metrics
```
┌─────────────────────────────────────────────────────────────┐
│                    SOFTWARE METRICS                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                   PRODUCT METRICS                       │ │
│  │                                                         │ │
│  │  Size: LOC, Function Points                             │ │
│  │  Complexity: Cyclomatic, Halstead                       │ │
│  │  Quality: Defect Density, Reliability                   │ │
│  │  Maintainability: Maintainability Index                │ │
│  └─────────────────────────────────────────────────────────┘ │
│                                                             │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │                  PROCESS METRICS                        │ │
│  │                                                         │ │
│  │  Productivity: LOC/person-month, FP/person-month       │ │
│  │  Quality: Defects/KLOC, Defect removal efficiency      │ │
│  │  Schedule: Schedule variance, Effort variance          │ │
│  │  Cost: Cost per function point, Budget variance        │ │
│  └─────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Product Metrics
- **Size Metrics**: Lines of Code (LOC), Function Points
- **Complexity Metrics**: Cyclomatic Complexity, Halstead Metrics
- **Quality Metrics**: Defect Density, Reliability Metrics
- **Maintainability Metrics**: Maintainability Index

### Process Metrics
- **Productivity**: LOC per person-month, Function Points per person-month
- **Quality**: Defects per KLOC, Defect removal efficiency
- **Schedule**: Schedule variance, Effort variance
- **Cost**: Cost per function point, Budget variance

### Benefits of Metrics
- **Measurement**: Quantify performance and quality
- **Control**: Monitor and control development process
- **Improvement**: Identify areas for improvement
- **Estimation**: Better project planning and estimation

---

## Quick Revision Points

### Key Models to Remember:
```
┌─────────────────────────────────────────────────────────────┐
│                    QUICK REFERENCE                          │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. Waterfall    → Sequential, rigid                        │
│  2. Prototyping  → User feedback, iterative                 │
│  3. RAD          → Fast, automated tools                    │
│  4. Incremental  → Small deliveries                         │
│  5. Spiral       → Risk-driven, iterative                   │
│  6. Component    → Reusable parts                           │
│  7. RUP          → Comprehensive, 4 phases                  │
│  8. Agile        → Flexible, customer-focused               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

1. **Waterfall** → Sequential, rigid
2. **Prototyping** → User feedback, iterative
3. **RAD** → Fast, automated tools
4. **Incremental** → Small deliveries
5. **Spiral** → Risk-driven, iterative
6. **Component** → Reusable parts
7. **RUP** → Comprehensive, 4 phases
8. **Agile** → Flexible, customer-focused

### CMM Levels (1-5):
```
┌─────────────────────────────────────────────────────────────┐
│                    CMM SUMMARY                              │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Level 1: Initial (Chaos)                                  │
│  Level 2: Repeatable (Basic PM)                            │
│  Level 3: Defined (Standardized)                           │
│  Level 4: Managed (Quantitative)                           │
│  Level 5: Optimizing (Continuous)                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

- **1**: Initial (Chaos)
- **2**: Repeatable (Basic PM)
- **3**: Defined (Standardized)
- **4**: Managed (Quantitative)
- **5**: Optimizing (Continuous)

### Agile Values:
```
┌─────────────────────────────────────────────────────────────┐
│                    AGILE VALUES                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Individuals > Processes                                    │
│  Working Software > Documentation                           │
│  Customer Collaboration > Contracts                         │
│  Responding to Change > Following Plans                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

- **Individuals** over processes
- **Working software** over documentation
- **Customer collaboration** over contracts
- **Responding to change** over following plans