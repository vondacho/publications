# BDD

**Behaviour-Driven Development** (BDD) is a software development technique with the central promise of facilitating shared understanding and optimising the functional quality of software deliveries.

![](images/img_common_understanding.png)

## Secure software development

This technique helps develop the right thing securely, i.e., the expected system behaviour, correct and complete, without causing functional regression.

## Contract-driven

This technique proposes a context for the **collaborative specification**, aiming to establish a shared understanding of the expected system behaviour and formalise it as a readable, **executable specification**s on which acceptance tests can be defined.

## Domain-driven

The issued specification artefact uses a natural-language domain-specific vocabulary that every stakeholder understands: product person, software, and test engineers.

## Documentation-driven

This artefact, written in Gherkin syntax, explains the system behaviour using examples grouped into scenarios that describe the system use cases and business rules.

Here is an example that uses a generic scenario to describe the behaviour of a problem-solving function; the Examples section defines the input and output values:

```gherkin
Feature: To mumble the letters of a text
 # See https://learn.madetech.com/katas/mumbling/

 Scenario Outline: Split a given text, repeating the letters, and capitalising the first occurrence only

   When mumbling <text>
   Then the result of mumbling is <result>
   Examples:
     | text   | result                     |
     | -      | -                          |
     | A      | A                          |
     | a      | A                          |
     | ab     | A-Bb                       |
     | abc    | A-Bb-Ccc                   |
     | abC    | A-Bb-Ccc                   |
     | aBCd   | A-Bb-Ccc-Dddd              |
     | QWERTY | Q-Ww-Eee-Rrrr-Ttttt-Yyyyyy |

```

More BDD scenarios: [Blueprint API](https://github.com/vondacho/arch-blueprint-kotlin/tree/master/src/acceptanceTest/resources/features)

## Test-driven

Coupled with **Acceptance Test-Driven Development** (ATDD), an outside-in software development technique, the software engineer automates test cases and can drive them to completeness, correctness, and the absence of functional regression during a feature increment.

BDD was initially introduced in 2003 by Dan North as a response to test-driven development (TDD), including acceptance testing or customer test-driven development practices found in extreme programming.

## Shift-left

BDD enables modern software development and promotes a shift-left approach in which both the Developer and the QA engineer contribute their perspectives to acceptance scenario mapping. The QA engineer's role can now better influence the completeness and the correctness of every delivery.
