## What is a View?
Views are projections of the software architecture

### Architecture View
Representation of a system from specific perspective

1. A system can be prepresentated in many views;
- Each with its **own, individual focus**
- In a view, **certain aspects are emphasised**, others are omitted
2. Specialization of the views helps better **handling of complexity**
3. View are **not entirely independent**
  - Certain information may show up in mulitple views
4. Views should be **consistent**
  - Should not contradict each other
 
![Views!](/views1.png)

## Context View
1. The system being designed is depicted as a black box
2. Shows relationships with **external actors** (e.g.; systems, users)
3. All interfaces to the outside world
   - **Interface types** (network, batch, USB, file, etc)
   - **Comms Protocols** (http, websockets,...)
   - **Comms Patterns** (sync/async, push/pull,...)
4. May provide an overview of the most important use cases of the system from an external perspective
5. Relevant for technical and non-technical stakeholders

## Building-Block View
1. Describes the **static decomposition** of the system into **building blocks**
   - Libraries, sub-systems, parititions, packages, classes, procedures, functions, etc
2. Describes the **relationhips** between building-blocks
   - Interfaces, dependencies, inheritance, associations, etc
3. Relevance
   - Helps stakeholders to understand the system (especially developers)
   - support project management with defining work packages

## Runtime View
1. Compliments Building-Block view, describing **interactions** between building blocks, participating in execution of a use case
2. Describes how the system components interact at **runtime**
3. Includes;
   - Processes and threads
   - how the system starts / terminates
   - which building block instances are available at runtime and their lifecycles
4. Relevance
   - Helps developers and testers understand how the system functions
   - Helps operations engineers so they can support prod
  
## Deploymnet View
1. Topology of technical infra
2. Describes deployment of run-time elements (apps, docker containers, dynamic libs to hardware components (servers, hosts, VMs, ...)
3. Includes logical and physical communication channels
4. Technical components (databases, servers, storage devices)  and their runtime attributes such as;
   - Availability
   - Network and memoery capacity, etc
5. Relevance
  - to communicate with operations (DevOps, SREs (Site Reliability Engineers), etc)
  - configure and manage run-time env
  - recognize bottlenecks, calculate costs, identify risks

## Example - Mobile Fitness App
![Views!](/views2.png)
![Views!](/views3.png)
![Views!](/views4.png)
![Views!](/views5.png)
![Views!](/views6.png)
![Views!](/views7.png)
![Views!](/views8.png)
![Views!](/views9.png)


