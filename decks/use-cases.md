---
marp: true
theme: gaia
_class: lead
paginate: true
author: Riccardo Cardin
lang: en
backgroundImage: url('../assets/background.png')
backgroundPosition: right 10px top 10px
backgroundSize: 150px
footer: "Software Engineering - Riccardo Cardin"
style: |
  section::after {
    content: 'Page ' attr(data-marpit-pagination) ' of ' attr(data-marpit-pagination-total);
    color:rgba(255, 246, 223, 1);
    height: 40pt;
    line-height: 30pt;
    font-size: 14pt;
  }
---

<!-- _paginate: skip -->

<style>
  section {
    font-size: 22pt;
  }
  header,footer {
    color:rgba(255, 246, 223, 1);
    background-color: rgba(169, 0, 35, 0.7);
    height: 40pt;
    line-height: 30pt;
  }
  h1, h2, h3, h4 {
    color:rgba(169, 0, 35, 1);
  }
  blockquote {
    font-size: 0.9em;
  }
  section > *  {
    font-size: 1em;
  }
</style>

<!-- _class: lead -->
# USE CASE DIAGRAMS

## SOFTWARE ENGINEERING

#### Università degli Studi di Padova
Dipartimento di Matematica
Corso di Laurea in Informatica

riccardo.cardin@unipd.it

---

## SUMMARY

- What are Use Cases
- Use Case Specification
- Use Case Diagrams
  - Use Case: Inclusion
  - Use Case: Extension
  - Use Case: Generalization

- Use Case Identification

---

<!-- _class: lead -->
# WHAT ARE USE CASES

---

## WHAT ARE USE CASES
**Techniques** for identifying **functional requirements**

**Describe interactions**
- System
- Users (actors) / external elements to the system

**How should the system be used?**
- What functionalities does it expose?

---

## EXAMPLE

An application is required that allows the management of a **simple blog**. 

In particular, at least all the basic functionalities of a blog must be available: 
- It must be possible for a user to **insert a new post**
- Subsequently, other users must be able to **comment on it**

These two operations must be available only to **registered users** within the system. 

Registration occurs by choosing a **username** and a **password**. The username must be **unique** within the system.

---

## WHAT ARE USE CASES
- Scenarios

  - **Sequence of steps that describe interactions**
    - Actors (users) and the system

  - **Representation of a possibility**
    - **Alternative** scenarios
      - Example: the credit card is not accepted, the customer is regular and their profile is already present in the system, …

  - **All scenarios (main and alternative) share a common goal**
    - Example: the purchase of at least one product

---

## WHAT ARE USE CASES
### Definition

**Informal**
> A use case is a situation in which the system is used to satisfy one or more user needs.

**Describe the set of system functionalities as perceived by users**
- External view of the system
- No implementation details

---

### FORMAL DEFINITION

> A use case is a set of scenarios (sequences of actions) that share a common final goal (objective) for a user (actor).

---

## WHAT ARE USE CASES
### Actors

**User's role in the interaction with the system**
- User: person, other external system
- "Physical" user → multiple roles (actors)
- Multiple users → same role (actor)

**Perform the use case to achieve the goal**
- Same actor → multiple use cases
- One use case → multiple actors

---

## IDENTIFYING ACTORS

**Good means of identifying use cases**

1. Identify the list of actors
2. Understand their goals and how they interact with the system (which role to which functionality)

⚠️ **No implementation details on interaction methods!**

---

<!-- _class: lead -->
# USE CASE SPECIFICATION

---

## USE CASE SPECIFICATION
### Use Cases are pure TEXT

**UML describes only use case diagrams**
- Specify the interaction between use cases

---

## SPECIFICATION EXAMPLE

**Use case:** UC1 - Registration
**Primary actor:** User
**Preconditions:** The user is not yet authenticated in the system
**Postconditions:** The user has an account in the system, characterized by a username and a password

**Main scenario:**
1. The user accesses the system
2. The user selects the "Register" functionality
3. The user enters a unique username in the system
4. The user enters a password that meets the imposed constraints

---

## SPECIFICATION EXAMPLE (continued)

**Extensions:**
a. In case the user enters a username already registered in the system:
   1. The user is not registered in the system
   2. An explanatory error is displayed
   3. The user is given the possibility to choose another password

---

## USE CASE SPECIFICATION
### The added value is in the textual content

- Name/Identifier
- Main scenario
- Alternative scenarios
  - Exception or error
- Pre-conditions
- Effects / Guarantee (post-conditions)
- Trigger
  - Triggering event of the use case
- Primary actors
- Secondary actors

---

## USE CASE SPECIFICATION
### Considerations

**Granularity**
- Satisfies the purpose of an actor (placing an order, …)
- Smaller than a business process

**Detail levels:**
- **Kite level** - Larger than a single operation on a component
- **Sea level** - Optimal level
- **Fish level** - Excessive detail that diverts focus from the objective

**Rules:**
- Only one main scenario per use case
- Alternative scenarios (0..*)
- Does not provide significant details, but identifies system functionalities

---

<!-- _class: lead -->
# USE CASE DIAGRAMS

---

## USE CASE DIAGRAMS
### Graphical representation of use cases

**Highlights actors and system services**

**Graph whose nodes are:**
- Actors
- Use cases

**Graph edges represent:**
- Communication between actors and use cases
- Links between use cases
  - Extension relationship
  - Inclusion relationship
  - Generalization relationship

**The diagram identifies system boundaries in the scenario**

---

## USE CASE DIAGRAM COMPONENTS

![width:800px center](use-case-components)

**Elements:**
- **Actor** (stick figure)
- **Use case** (oval)
- **Association** (simple line)
- **Inclusion** (`«include»`)
- **Extension** (`«extend»`)
- **Generalization** (empty arrow)

The use case name can be positioned inside or outside the figure

---

## EXAMPLE - ASSOCIATION

**Actor - use case association: participation**

![width:700px center](blog-example)

```
┌─────────┐
│  User   │────────► ( UC1 - Registration )
└─────────┘  executes
              
    Blog System Boundary
```

- Direct communication
- System utilization
- **MUST also be described in TEXTUAL version**
  - Preconditions and postconditions cannot be inferred

---

## EXAMPLE - COMPONENTS

![width:800px center](use-case-structure)

```
         actor
           │
           │ participates
           ▼
    ( use case )
           │
        ┌──┴──┐
      subject
```

---

<!-- _class: lead -->
# USE CASE: INCLUSION

---

## USE CASE: INCLUSION
### Common functionality among multiple use cases

**Every instance of A executes B**
- B is unconditionally included in the execution of A
- A does not know the details of B, only its results
- B does not know it is included by A
- Responsibility for B's execution is entirely with A

**Advantages:**
- Avoids repetition
- Increases reusability

```
    ( A )────«include»────►( B )
```

---

## EXAMPLE - INCLUSION

![width:900px center](inclusion-example)

⚠️ **Important:** The database must be external to the system boundary (i.e. Facebook, Twitter)!!!

---

<!-- _class: lead -->
# USE CASE: EXTENSION

---

## USE CASE: EXTENSION
### Increasing use case functionalities

**Every instance of A executes B conditionally**
- B's execution interrupts A
- Responsibility for extension cases belongs to the extender (B)

⚠️ **Does not represent inheritance in programming languages**

```
    ( A )◄────«extend»────( B )
```

---

## USE CASE: EXTENSION
### Characteristics

**Extension condition**
- Determines when the extension should be used
- Narrative description and/or use case icon
- The extension condition is verified

**Properties:**
- Can exist independently of extended use cases
- Can extend multiple base use cases (reuse)

⚠️ **Attention to the extended use case boundary**
- Modifies main scenario / post condition

**Example:** exception case handling

---

## EXAMPLE - EXTENSION

![width:900px center](extension-example)

---

<!-- _class: lead -->
# INCLUSION AND EXTENSION

---

## INCLUSION AND EXTENSION
### Common aspects and differences

**Common aspects:**
- Factor common behaviors across multiple use cases
- Enhance the behavior of a base use case

**Differences:**

| Extension | Inclusion |
|------------|------------|
| The actor may **not execute** all extensions (conditions not verified) | The actor **always** executes all inclusions |
| Describes **variations** from standard functionality | A functionality **repeats** across multiple use cases |

---

<!-- _class: lead -->
# USE CASE: GENERALIZATION

---

## USE CASE: GENERALIZATION
### Adding or modifying base characteristics

**Actors**
- A is a generalization of B if B shares at least A's functionalities

**Use Cases (rarer)**
- Child use cases can add functionalities compared to parents, or modify their behavior
- All functionalities not redefined in the child are maintained as defined in the parent

![width:600px center](generalization-examples)

---

## EXAMPLE - GENERALIZATION

![width:900px center](generalization-example)

---

<!-- _class: lead -->
# USE CASE: COMPLETE EXAMPLE

---

## CASE STUDY: TRIPADVISOR

Tripadvisor is a well-known travel site widespread throughout the world. To access it, it is necessary to **register** by providing a username and password. As in many other systems, the username must be **unique**: the system, therefore, does not allow a new user to register using a username already chosen by another user.

The site contains reviews of numerous tourist attractions, restaurants, hotels, etc...

---

## CASE STUDY: TRIPADVISOR (continued)

**Reviews** are publicly visible and can be read even by unregistered users. Writing reviews is available only to registered users.

Each review contains a **summary rating** that the user enters using "stars" (from one to five) and a description of at least 100 characters. If a user tries to insert a review of shorter length, the system alerts the user with an **error message**.

It is possible for the **owner** of the tourist attraction to briefly respond to a review, inserting a comment in turn.

---

## CASE STUDY: TRIPADVISOR (continued)

A user's **profile** is characterized not only by their name and photo, which can be modified, but also by the badges they have obtained.

**Badges** are linked to the number of reviews written: for example, after 20 reviews the user becomes an "Expert Reviewer" and the system notifies them with an appropriate message.

It is finally possible to **connect** one's account with one's Facebook profile. In this case, the system will notify the user whenever a friend inserts a review on Tripadvisor.

---

## TRIPADVISOR DIAGRAM

![width:1000px center](tripadvisor-diagram)

---

<!-- _class: lead -->
# USE CASE IDENTIFICATION

---

## USE CASE IDENTIFICATION
### Context definition

1. **Actor and responsibility identification**
2. **Goal identification** to be achieved for each actor
   - First approximation of use cases
3. **Evaluate actors and use cases and refine them**
   - Division and merging
4. **Find inclusion relationships**
5. **Find extension relationships**
6. **Find generalization relationships**

> «A use case is something that provides some measurable result to the user on an external system»

---

## USE CASE IDENTIFICATION
### How far should the level of detail go?

**Kite level**
- Very abstract level, defines macro functionalities

**Sea level**
- Intermediate level, useful in discovering hidden functionalities

**Fish level**
- Detail level, from which system requirements are directly identified

---

<!-- _class: lead -->
# REFERENCES

---

## REFERENCES

- **OMG Homepage** – www.omg.org
- **UML Homepage** – www.uml.org
- **UML Distilled**, Martin Fowler, 2004, Pearson (Addison Wesley)
- **Learning UML 2.0**, Kim Hamilton, Russell Miles, O'Reilly, 2006

---

## GITHUB REPOSITORY

https://github.com/rcardin/swe

---

<!-- _class: lead -->
# THANK YOU FOR YOUR ATTENTION

**Questions?**