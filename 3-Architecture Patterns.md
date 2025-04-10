# Introduction and Motivation
Libraries allow us to reuse code. Frameworks allow us to reuse structure.

Patterns allow us to reuse thinking.
- Apply solutions to problems in different domains
- Apply solutions to different levels of abstraction

## Patterns
- Describe   reusable (abstract or concrete) solutions to common problems
- Provide a recognizable structure and terminology for those solutions

> Patterns are discovered, not invented. Universe is full of them.

## Designing with Patterns
Patterns offer approaches for
- Decomposition  of a system
- Distribution of responsibilities within a system

# Layers Pattern
## Introduction
System is structured into stacked layers of services. 
### Each Layer;
- Encapsulates details
- May provide abstraction
- Provides services to layers above it

### Dependencies
- Can depend on layers below it
- Cannot depend on layers above it

### Usage
- Directed from upper to lower layer

### Communication
- Can be directed in both ways

## Examples
### OSI (Open Systems Interconnection) Model
![ISO OSI!](/iso_osi.png)

### Multi-Layered / N-Layered Monolith Architecture
Web Architecture
![Web Arch!](/web_arch.png)

### Multi-Tiered Architecture
Each tier runs in its own process, and even separate computer.
3-Tiered Architecture
![3 tiered!](/three_tiered.png)
![3 tiered plus layered!](/three_tiered_layered.png)

## Closed-Layered Architecture vs. Open Layered

## Pros and Cons
