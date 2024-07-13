# Views

## Introduction

We will adopt the combination of two architectural representation models: C4 and 4+1.

### 4 + 1 View Model

The 4+1 view model is a proposes the description of the system through complementary views, each one with a specific 
purpose. This way allows the perception of the system from different perspectives, which facilitates the understanding
of the system as a whole.

The views are:

* **Logical View**: It's goal is to answer to business challenges/requirements regarding software aspects.
* **Process View**: Demonstrates the system's flow and interactions.
* **Development View**: Regards the software organization in its development environment.
* **Physical View**: Maps the various software elements to the hardware components, per example, where the software
is executed.
* **Scenery View**: Represents the association between the business processes and the actors that will trigger them.

### C4 Model

The C4 model defends the description of software using four levels of abstraction: system context, containers, 
components and code. Each one adopts a thinner layer of granularity, which allows the more detailed description 
of the system in smaller parts. We can think of it as a zoom in the system.

The levels are:

* **System Context**: It's the highest level of abstraction, and it's goal is to demonstrate the system's scope.
* **Containers**: Describe system containers.
* **Components**: Describe containers components.
* **Code**: Describe components code or even more detailed components.

### Overview

By combining the two models it is possible to represent the system in various perspectives, each one with different
levels of detail.

To represent/modulate, the implemented as well as thought solutions, we will use Unified Modeling Language (UML) as 
the notation.

## Glossary

- [Glossary](Glossary.md)

## Individual Views

- [DAM Views](DAMViews.md)
- [PM Views](PMViews.md)
- [RPM Views](RPMViews.md)
- [UM Views](UMViews.md)

## Level 1

### Logical View

![Logical View](diagrams/SPRINT_C/level1/Logical.svg)

### Implementation View

![Implementation View](diagrams/SPRINT_C/level1/Implementation.svg)

### Process View

#### POST
![Process View](diagrams/SPRINT_C/level1/process-views/create/Generic_Create.svg)

#### GET
![Process View](diagrams/SPRINT_C/level1/process-views/list-all/Generic_List_All.svg)

#### PATCH
![Process View](diagrams/SPRINT_C/level1/process-views/edit/Generic_Edit.svg)

#### CREATE SIGNUP REQUEST
![Process View](diagrams/SPRINT_C/level1/process-views/signup/Signup.svg)

#### ACCEPT SIGNUP REQUEST
![Process View](diagrams/SPRINT_C/level1/process-views/accept-signup-request/AcceptSignupRequest.svg)

#### LOGIN / REDIRECT
![Process View](diagrams/SPRINT_C/level1/process-views/login/Login.svg)

---

### Level 2

#### Logical View

![Logical View](diagrams/SPRINT_C/level2/Logical.svg)


#### Implementation View

![Implementation View](diagrams/SPRINT_C/level2/Implementation.svg)


#### Physical View

![Physical View](diagrams/SPRINT_C/level2/Physical.svg)

- With the orange color we represent a component that is not part of the solution, but it will use RobDroneGo system.
- With the blue color we represent the components that are part of the system, and are supposed to be developed by the team.

#### Process View

##### POST
![Process View](diagrams/SPRINT_C/level2/process-views/create/Generic_Create.svg)

##### GET
![Process View](diagrams/SPRINT_C/level2/process-views/list-all/Generic_List_All.svg)

##### PATCH
![Process View](diagrams/SPRINT_C/level2/process-views/edit/Generic_Edit.svg)

##### ACCEPT SIGNUP REQUEST
![Process View](diagrams/SPRINT_C/level2/process-views/accept-signup-request/AcceptSignupRequest.svg)

##### CREATE BACKOFFICE USER
![Process View](diagrams/SPRINT_C/level2/process-views/create-user/CreateBackofficeUser.svg)

---

### Level 3

#### Logical View - RobDroneGo Portal Module

![Logical View](diagrams/SPRINT_C/level3/RPM/LogicalRpm.svg)


#### Implementation View - RobDroneGo Portal Module

![Implementation View](diagrams/SPRINT_C/level3/RPM/ImplementationRpm.svg)

#### Process View - RobDroneGo Portal Module

##### List All

![Process View](diagrams/SPRINT_C/level3/RPM/process-views/list-all/Generic_List_All.svg)

##### List Filter

![Process View](diagrams/SPRINT_C/level3/RPM/process-views/list-filters/Generic_List_Filters.svg)

##### Edit

![Process View](diagrams/SPRINT_C/level3/RPM/process-views/edit/Generic_Edit.svg)

##### Create

![Process View](diagrams/SPRINT_C/level3/RPM/process-views/create/Generic_Create.svg)

---

#### Logical View - Data Administration Module

![Logical View](diagrams/SPRINT_C/level3/DAM/LogicalDam.svg)


#### Implementation View - Data Administration Module

![Implementation View](diagrams/SPRINT_C/level3/DAM/ImplementationDam.svg)

#### Process View - Data Administration Module

##### POST - Building
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-150/US150-PV.svg)

##### POST - Robisep
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-360/US360-PV.svg)

##### POST - Passage
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-240/US240-PV.svg)


#### PATCH - Elevator
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-280/US280-PV.svg)

#### PATCH - Floor
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-200&US-230/US200&US230-PV.svg)

#### PATCH - Passage
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-250/US250-PV.svg)

##### PATCH - Robisep
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-370/US370-PV.svg)


##### GET - Robisep
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-380/US380-PV.svg)

##### GET - Passage
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-260/US260-PV.svg)

##### GET - Task Sequence
![Process View](diagrams/SPRINT_C/level3/DAM/process-views/US-500/US500-PV.svg)

---

#### Logical View - Planning Module

![Logical View](diagrams/SPRINT_C/level3/PM/LogicalPm.svg)


#### Implementation View - Planning Module

![Implementation View](diagrams/SPRINT_C/level3/PM/ImplementationPm.svg)

#### Process View - Planning Module

##### List - Paths

![Process View](diagrams/SPRINT_C/level3/PM/US510/US510-PV.svg)

##### List - Task Sequence

![Process View](diagrams/SPRINT_C/level3/PM/US500/US500-PV.svg)

---

#### Logical View - User Management Module

![Logical View](diagrams/SPRINT_C/level3/UM/LogicalUm.svg)


#### Implementation View - User Management Module


![Implementation View](diagrams/SPRINT_C/level3/UM/ImplementationUm.svg)


#### Process View - User Management Module

##### CREATE BACKOFFICE USER
![Process View](diagrams/SPRINT_C/level3/UM/process-views/create-user/CreateBackofficeUser.svg)

##### ACCEPT SIGNUP REQUEST
![Process View](diagrams/SPRINT_C/level3/UM/process-views/accept-signup-request/AcceptSignupRequest.svg)