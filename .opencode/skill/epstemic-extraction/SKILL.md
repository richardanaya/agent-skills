---
name: epistemic-extraction
description: An epistemic extraction system that analyzes text to identify its logical structure according to Aristotelian and Objectivist epistemology. Your task is to extract concepts, propositions, and arguments from provided text.
license: MIT
compatibility: opencode
metadata:
  audience: thinks
  philosophy: aristotle, ayn rand
---

# Epistemic Extraction System

## Theoretical Framework

The extraction follows this hierarchy:

- **Percepts** ground **concepts**
- **Concepts** compose **propositions**
- **Propositions** compose **arguments**

Each level has its own standards:

- Concepts must be properly formed (valid abstraction, essential definitions)
- Propositions must assert something that can be true or false
- Arguments must have valid logical form

## Extraction Components

### Concepts

A concept is an open-ended mental integration of concretes according to their essential characteristics. Extract the key terms the text relies upon to make its claims.

For each concept, identify its **essentials**—the attributes which explain the most about the entity. A concept may have multiple essentials.

**Guidelines for essentials:**

- Use plain language a general dictionary would use
- Avoid jargon or technical terminology unless necessary
- Keep phrases clear and concise
- Capture both genus and differentia where applicable

### Propositions

A proposition is a statement that asserts or denies something of something—one that is capable of being true or false. Extract only **universal propositions** from the text.

**Proposition types:**

- **universal_affirmative**: "All S are P"
- **universal_negative**: "No S is P"

**Guidelines for propositions:**

- Do not use pronouns; resolve all references to their specific referents
- Use plain language with clear meaning
- Each proposition should be atomic (one claim per proposition)
- Extract the implicit universal claims the text relies upon, not just explicit statements

### Arguments

An argument is a set of propositions where some (premises) support another (conclusion). Identify the logical structures in the text.

**Guidelines for arguments:**

- State all premises as full propositions, not as references or numbers
- Name each argument descriptively
- Identify the logical form where applicable (Barbara, Celarent, Sorites, Conjunction, etc.)
- Include both explicit and implicit premises the argument relies upon
- State conclusions in plain language

## Output Format

Return a JSON object conforming to the schema defined at the end of this document.

## Extraction Principles

1. **Charity**: Interpret the text in its strongest reasonable form
2. **Completeness**: Extract implicit premises and universal claims the text assumes
3. **Clarity**: Use simple, dictionary-standard language throughout
4. **Atomicity**: Break complex claims into their constituent propositions
5. **Hierarchy**: Recognize that arguments depend on propositions, which depend on concepts

## Common Logical Forms

- **Barbara** (AAA-1): All M are P; All S are M; Therefore all S are P
- **Celarent** (EAE-1): No M is P; All S are M; Therefore no S is P
- **Sorites**: A chain of syllogisms where the conclusion of each is a premise of the next
- **Conjunction**: Two premises combined to yield a joint conclusion
- **Modus Ponens**: If P then Q; P; Therefore Q
- **Modus Tollens**: If P then Q; Not Q; Therefore not P

---

## JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "EpistemicExtraction",
  "description": "Schema for epistemic extraction of concepts, propositions, and arguments from text",
  "type": "object",
  "required": ["concepts", "propositions", "arguments"],
  "properties": {
    "concepts": {
      "type": "array",
      "description": "Key terms the text relies upon to make its claims",
      "items": {
        "type": "object",
        "required": ["term", "essentials"],
        "properties": {
          "term": {
            "type": "string",
            "description": "The concept word or phrase"
          },
          "essentials": {
            "type": "array",
            "description": "Attributes which explain the most about the entity",
            "items": {
              "type": "string"
            },
            "minItems": 1
          }
        }
      }
    },
    "propositions": {
      "type": "array",
      "description": "Universal statements that assert or deny something",
      "items": {
        "type": "object",
        "required": ["type", "statement"],
        "properties": {
          "type": {
            "type": "string",
            "enum": ["universal_affirmative", "universal_negative"],
            "description": "The logical type of the proposition"
          },
          "statement": {
            "type": "string",
            "description": "The full proposition in plain language without pronouns"
          }
        }
      }
    },
    "arguments": {
      "type": "array",
      "description": "Logical structures where premises support conclusions",
      "items": {
        "type": "object",
        "required": ["name", "premises", "conclusion", "form"],
        "properties": {
          "name": {
            "type": "string",
            "description": "A descriptive name for the argument"
          },
          "premises": {
            "type": "array",
            "description": "Full proposition statements serving as premises",
            "items": {
              "type": "string"
            },
            "minItems": 1
          },
          "conclusion": {
            "type": "string",
            "description": "The proposition that follows from the premises"
          },
          "form": {
            "type": "string",
            "enum": [
              "Barbara",
              "Celarent",
              "Darii",
              "Ferio",
              "Cesare",
              "Camestres",
              "Festino",
              "Baroco",
              "Darapti",
              "Disamis",
              "Datisi",
              "Felapton",
              "Bocardo",
              "Ferison",
              "Sorites",
              "Conjunction",
              "Modus Ponens",
              "Modus Tollens",
              "Disjunctive Syllogism",
              "Hypothetical Syllogism",
              "Reductio ad Absurdum"
            ],
            "description": "The logical form of the argument"
          }
        }
      }
    }
  }
}
```