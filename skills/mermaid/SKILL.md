---
name: mermaid
description: Used only if user wants to see diagrams. Provides information about how to choose diagram style, how to build it, and which patterns to follow.
allowed-tools: Read, Write
user-invocable: false
---

## Purpose

The skill contains information necessary for quality diagram building. Diagrams are an indispensable form
of explaining codebase functionality to the user.

## Rules

1. All diagrams are described ONLY in `mermaid` format
2. No more than 3 diagrams can be described in a file. If you see that 3 diagrams are already described - don't start building a new one.
3. Don't use other diagram types not described in this skill.
4. Leave comments in diagrams in the same language the user communicates in.

## Diagram Types

Several diagram types are available to the agent for building:

1. **sequenceDiagram**
   Description: shows the sequence of data transfer between components.
   Used for: explaining interaction of multiple components in a large research block.
   Example:
    ```mermaid
        sequenceDiagram
            Fragment->>+ViewModel: InitialIntent
            Fragment->>+ViewModel: Subscribe state
            ViewModel->>+Repository: LoadData
            Repository-->>ViewModel: Dto
            ViewModel-->>ViewModel: Update state
            ViewModel-->>Fragment: State
    ```
2. **flowchart**
   Description: Logic flowchart with conditions and branches.
   Used for: explaining function operation; explaining heavy decision-making logic in the studied code.
   Example:
   ```mermaid
      flowchart TD
        A[Start] --> B{Authorized?}
        B -->|Yes| C[Load data]
        B -->|No| D[Open login]
   ```
3. **dependency graph**
   > For its description in `mermaid`, use `graph TD`.

   Description: graph showing dependencies between modules, components, or system layers.
   Used for: explaining dependencies in project/module/feature. Very useful for understanding the system as a whole.
   Example:
   ```mermaid
      graph TD
        App --> AuthAPI
        AuthAPI --> AuthImpl
        AuthImpl --> CoreNetwork
   ```
4. **class diagram**
   > Use if you need to explicitly describe class properties, otherwise prefer `dependency graph`.

   Description: shows classes, interfaces, and relationships between them.
   Used for: understanding model architecture, contracts, and object dependencies.
   Example:
   ```mermaid
      classDiagram
        Animal <|-- Duck
        Animal <|-- Fish
        Animal <|-- Zebra
        Animal : +int age
        Animal : +String gender
        Animal: +isMammal()
        Animal: +mate()
        class Duck{
            +String beakColor
            +swim()
            +quack()
        }
        class Fish{
            -int sizeInFeet
            -canEat()
        }
        class Zebra{
            +bool is_wild
            +run()
        }
   ```
5. **ER diagram**
   > Use only if you need to explicitly study databases.

   Description: entity-relationship schema for data and their connections.
   Used for: database structure or domain storage models.
   Example:
   ```mermaid
      erDiagram
        CUSTOMER ||--o{ ORDER : places
        ORDER ||--|{ ORDER_ITEM : contains
        PRODUCT ||--o{ ORDER_ITEM : includes
        CUSTOMER {
            string id
            string name
            string email
        }
        ORDER {
            string id
            date orderDate
            string status
        }
        PRODUCT {
            string id
            string name
            float price
        }
        ORDER_ITEM {
            int quantity
            float price
        }
   ```

## How to Choose a Diagram

1. If database was studied - **ER diagram**
2. If function operation or complex decision-making logic was studied - **flowchart diagram**
3. If class properties and class relationships needed to be studied - **class diagram**
4. If data flow, user path, or component interaction needed to be described - **sequence diagram**
5. If component relationships in module, package, application needed to be described - **dependency graph**

> Important: usually 3 different diagrams are built for explanation, so if you already chose one type (e.g., flowchart),
> diversify the description and choose a different diagram next.