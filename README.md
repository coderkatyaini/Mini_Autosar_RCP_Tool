# Mini AUTOSAR RCP Tool

A simplified Eclipse RCP-based AUTOSAR tooling application designed to demonstrate how an AUTOSAR-oriented desktop application can import ARXML files, display ECU configuration data in a hierarchical tree, validate configuration elements, show properties, and generate C source and header files from the imported configuration.
This project is being developed as a learning and portfolio project to understand **Java, Eclipse RCP, Eclipse e4, SWT, JFace, EMF, XML/ARXML processing, validation, and code generation** in an AUTOSAR tooling environment.

---

## Project Overview

**Mini_Autosar_RCP_Tool** is a lightweight implementation inspired by professional AUTOSAR configuration and development tools.

The application provides a graphical desktop interface where a user can:

1. Load an AUTOSAR `.arxml` file.
2. Parse the ARXML content.
3. Display AUTOSAR elements in a hierarchical Tree Viewer.
4. Select an element and inspect its properties.
5. Validate the imported configuration.
6. Display validation results.
7. Filter validation results.
8. Search for elements.
9. Generate simplified `.c` and `.h` files from the configuration.

The main objective is to understand the architecture behind an Eclipse-based automotive development tool while keeping the implementation small enough to develop and understand independently.

---

## Project Objectives

The main objectives of this project are:

- Learn Eclipse RCP application development.
- Understand Eclipse e4 application architecture.
- Practice Java desktop application development.
- Learn SWT and JFace UI development.
- Understand Eclipse ViewParts and Perspectives.
- Work with `TreeViewer` and `TableViewer`.
- Parse XML/ARXML files.
- Understand basic AUTOSAR data structures.
- Implement configuration validation.
- Implement property inspection.
- Implement search and filtering.
- Implement C/C++ code generation.
- Understand separation between UI, model, validation and generation layers.
- Build a portfolio project demonstrating AUTOSAR tooling knowledge.

---

# Architecture

The project follows a layered architecture.

.
                    +----------------------+
                    |      User / UI       |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    |     Eclipse RCP      |
                    |       e4 / SWT       |
                    +----------+-----------+
                               |
             +-----------------+----------------+
             |                 |                |
             v                 v                v
      +-------------+   +-------------+   +-------------+
      | ARXML       |   | Validation  |   | Properties  |
      | Importer    |   | Engine      |   | Manager     |
      +------+------+   +------+------+   +-------------+
             |                 |
             v                 v
      +----------------------------------+
      |          AUTOSAR Model           |
      +----------------+-----------------+
                       |
                       v
              +-------------------+
              | Code Generator    |
              +---------+---------+
                        |
                +-------+-------+
                |               |
                v               v
              .c files         .h files
```

---

# 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Java | Core application development |
| Eclipse RCP | Rich Client desktop application |
| Eclipse e4 | Application model and dependency injection |
| SWT | GUI development |
| JFace | Viewers, dialogs and UI utilities |
| Maven | Build and dependency management |
| Tycho | Eclipse/OSGi build |
| EMF | Model representation |
| XML | ARXML processing |
| AUTOSAR ARXML | Automotive configuration input |
| Xtend / Templates | Code generation |
| Git | Version control |
| GitHub | Source-code hosting |

---

# AUTOSAR Context

AUTOSAR (AUTomotive Open System ARchitecture) is a standardized software architecture used in the automotive industry.

This project does not attempt to implement the complete AUTOSAR specification.

Instead, it implements a simplified subset of AUTOSAR concepts to demonstrate the workflow of an automotive configuration tool.

The simplified workflow is:

```text
ARXML
  |
  v
Import
  |
  v
Parse XML
  |
  v
Build AUTOSAR Model
  |
  +---------> Tree Viewer
  |
  +---------> Properties View
  |
  +---------> Validation View
  |
  v
Code Generation
  |
  +---------> .c
  |
  +---------> .h
```

---

# Project Features

## 1. ARXML Import

The application allows users to select an AUTOSAR `.arxml` file from the local system.

Example:

```text
File
 |
 +-- Open ARXML
       |
       +-- ECU Configuration.arxml
```

The imported file is parsed and converted into an internal model.

---

## 2. AUTOSAR Tree Viewer

The imported AUTOSAR elements are displayed hierarchically using Eclipse JFace `TreeViewer`.

Example:

```text
AUTOSAR Project
│
├── ECUC-MODULE-CONFIGURATION-VALUES
│   │
│   ├── Module A
│   │   ├── Parameter A
│   │   └── Parameter B
│   │
│   └── Module B
│       ├── Parameter C
│       └── Parameter D
│
├── SWC
│   ├── Component A
│   └── Component B
│
└── System
    ├── Network
    └── ECU
```

The tree structure is designed to demonstrate how complex AUTOSAR configuration data can be represented in an IDE-like environment.

---

# Properties View

When the user selects an element from the Tree Viewer, its properties are displayed in a Properties View.

Example:

```text
Selected Element
-------------------------
Short Name : EngineControl
Type       : ECUC-MODULE
Origin     : ARXML
Value      : Enabled
```

The Properties View helps users inspect configuration elements without navigating through the original XML.

---

# Validation View

The application provides a validation mechanism for detecting invalid or inconsistent configuration data.

Example validation results:

```text
Element          Result          Type
------------------------------------------------
ModuleA          Valid           Configuration
ModuleB          Error           Parameter
ParameterX      Warning          Value
```

Possible validation levels:

- Information
- Warning
- Error

---

# Validation Filtering

The Validation View supports filtering based on:

- Severity
- Element type
- Result type
- Search text

Example:

```text
Severity:
[All]
[Error]
[Warning]
[Information]
```

Users can therefore focus on specific validation problems.

---

# Search

The application provides search functionality for finding elements within the loaded AUTOSAR model.

Example:

```text
Search: Engine

Results:

EngineControl
EngineSpeed
EngineConfiguration
```

---

# Code Generation

The project includes a simplified code-generation mechanism.

Based on the imported AUTOSAR configuration, the application generates:

```text
Generated/
│
├── MiniAutosar_Config.h
└── MiniAutosar_Config.c
```

Example generated header:

```c
#ifndef MINI_AUTOSAR_CONFIG_H
#define MINI_AUTOSAR_CONFIG_H

#define ENGINE_CONTROL_ENABLED 1
#define MAX_ENGINE_SPEED 6000

#endif
```

Example generated source:

```c
#include "MiniAutosar_Config.h"

void MiniAutosar_Init(void)
{
    /* Generated initialization code */
}
```

The generated code is intentionally simplified and is not intended to be production AUTOSAR code.

---

# Proposed Project Structure

```text
Mini_Autosar_RCP_Tool
│
├── README.md
├── pom.xml
│
├── bundles/
│   │
│   ├── com.example.mini.autosar.model
│   │
│   ├── com.example.mini.autosar.parser
│   │
│   ├── com.example.mini.autosar.validation
│   │
│   ├── com.example.mini.autosar.generator
│   │
│   └── com.example.mini.autosar.ui
│
├── features/
│   └── com.example.mini.autosar.feature
│
├── releng/
│   └── target-platform
│
├── configuration/
│
├── examples/
│   └── sample.arxml
│
└── generated/
    ├── MiniAutosar_Config.c
    └── MiniAutosar_Config.h
```

The exact package structure may evolve during development.

---

# Main Components

## UI Layer

Responsible for:

- Application window
- Menus
- Toolbars
- Tree Viewer
- Properties View
- Validation View
- Dialogs
- Filters
- User interaction

Technologies:

```text
Eclipse e4
SWT
JFace
```

---

## ARXML Parser

Responsible for:

- Reading ARXML files
- Parsing XML
- Extracting AUTOSAR elements
- Creating internal model objects

Example:

```text
ARXML
  ↓
XML Parser
  ↓
AUTOSAR Model
```

---

## Model Layer

Represents AUTOSAR configuration objects.

Example:

```java
AutosarElement
    |
    +-- name
    +-- type
    +-- value
    +-- children
    +-- properties
```

---

## Validation Layer

Responsible for checking:

- Missing required values
- Invalid values
- Duplicate elements
- Invalid references
- Unsupported configuration
- Structural problems

Example:

```java
ValidationResult
{
    element
    severity
    message
    resultType
}
```

---

## Code Generator

Responsible for converting the internal model into source code.

```text
AUTOSAR Model
      |
      v
Generator
      |
      +------> .h
      |
      +------> .c
```

---

# User Interface

The planned application layout is:

```text
+-------------------------------------------------------------+
