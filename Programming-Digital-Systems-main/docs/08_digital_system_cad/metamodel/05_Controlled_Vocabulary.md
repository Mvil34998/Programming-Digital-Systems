# Controlled Vocabulary

## 1. Назначение документа

`05_Controlled_Vocabulary.md` описывает правила controlled vocabulary для рабочей метамодели Digital System CAD.

Controlled vocabulary нужен, чтобы термины модели были стабильными, проверяемыми и пригодными для SDD, реестров, views, transformations и Codex context.

> [!info] Главное
> Имя не является определением. Важный термин должен иметь Definition, Context, Source, допустимые синонимы, запрещённые синонимы и границы применения.

## 2. Почему это важно

Без controlled vocabulary модель быстро ломается:

- один термин начинает означать разные вещи;
- разные термины начинают означать одно и то же;
- имя используется вместо определения;
- доменные термины смешиваются с универсальными элементами;
- view начинает вводить новый смысл без факта модели;
- Codex получает неоднозначный контекст.

Controlled vocabulary нужен не ради словаря, а ради стабильной модели.

## 3. Что является term

Term — это значимое слово или выражение, которое используется в модели, документации, реестрах, SDD, views, relation types или Codex context.

Term может описывать:

- element type;
- relation type;
- field;
- status;
- validation severity;
- view;
- transformation;
- domain concept;
- architecture concept;
- implementation artifact;
- forbidden synonym;
- profile-specific extension.

## 4. Что не является достаточным term

Недостаточно просто записать:

```text
Entity
Rule
Flow
Module
Integration
```

Такая запись является только именем.

Для controlled vocabulary нужно:

```text
Term + Definition + Context + Boundaries + Source
```

## 5. Универсальная форма term

```yaml
id:
term:
status:
definition:
context:
scope:
allowed_synonyms:
forbidden_synonyms:
not_examples:
related_element_types:
related_relation_types:
related_fields:
source:
used_in:
open_questions:
```

Поля:

| Поле | Назначение |
|---|---|
| `id` | стабильный ID термина |
| `term` | основное имя |
| `status` | статус термина |
| `definition` | определение |
| `context` | где термин применяется |
| `scope` | границы применения |
| `allowed_synonyms` | допустимые синонимы |
| `forbidden_synonyms` | запрещённые синонимы |
| `not_examples` | что термином не является |
| `related_element_types` | связанные element types |
| `related_relation_types` | связанные relation types |
| `related_fields` | связанные поля |
| `source` | источник определения |
| `used_in` | где термин используется |
| `open_questions` | неоднозначности |

## 6. Статусы term

| Статус | Значение |
|---|---|
| `draft` | термин записан предварительно |
| `candidate` | термин используется как рабочий кандидат |
| `accepted` | термин принят в текущей модели |
| `profile-specific` | термин допустим только в доменном профиле |
| `deprecated` | термин больше не рекомендуется |
| `forbidden` | термин запрещён как неоднозначный или неправильный |

На текущем этапе большинство терминов имеют статус `candidate`.

## 7. ID terms

Предварительный формат:

```text
TERM-<AREA>-<NUMBER>
```

Примеры:

```text
TERM-MODEL-001
TERM-REL-001
TERM-VIEW-001
TERM-SDD-001
TERM-ARCH-001
TERM-DOMAIN-001
```

## 8. Core modeling terms

### 8.1. Model

```yaml
id: TERM-MODEL-001
term: Model
status: candidate
definition: "A structured description of a concrete system or part of a system built from typed elements, typed relations, structured facts and validation rules."
context: "Digital System CAD M1 level"
scope: "Concrete system descriptions"
allowed_synonyms:
  - "system model"
forbidden_synonyms:
  - "diagram"
  - "document"
  - "table"
not_examples:
  - "SDD document without structured facts"
  - "diagram without element IDs"
related_element_types:
  - TYPE-MODEL
related_relation_types:
  - REL-CONFORMS-TO
  - REL-CONTAINS
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "Metamodel Form"
  - "Structured Facts"
  - "SDD From Model"
open_questions:
  - "What is the minimal storage format for the early model repository?"
```

### 8.2. Metamodel

```yaml
id: TERM-MODEL-002
term: Metamodel
status: candidate
definition: "Rules for creating models, including allowed element types, relation types, fields, validation rules, views and transformations."
context: "Digital System CAD M2 level"
scope: "Rules of model construction"
allowed_synonyms:
  - "modeling rules"
forbidden_synonyms:
  - "model"
  - "application"
  - "diagram editor"
not_examples:
  - "a model of one concrete system"
related_element_types:
  - TYPE-MODEL
  - TYPE-VALIDATION-RULE
related_relation_types:
  - REL-CONFORMS-TO
source:
  - "docs/08_digital_system_cad/research/01_Metamodeling_Methods_And_Standards.md"
used_in:
  - "Model Elements"
  - "Model Relations"
open_questions:
  - "How formal should the first metamodel version be?"
```

### 8.3. Element Type

```yaml
id: TERM-MODEL-003
term: Element Type
status: candidate
definition: "A type of model element allowed by the metamodel."
context: "M2 metamodel definition"
scope: "Types such as Entity, DataField, Rule, Event, Flow, Interface"
allowed_synonyms:
  - "model element type"
forbidden_synonyms:
  - "class"
  - "table"
  - "diagram block"
not_examples:
  - "a concrete entity in one project"
related_element_types:
  - TYPE-MODEL
related_relation_types:
  - REL-CONFORMS-TO
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "Metamodel Form"
open_questions: []
```

### 8.4. Model Element

```yaml
id: TERM-MODEL-004
term: Model Element
status: candidate
definition: "A concrete typed object in a model, identified by stable ID and described by fields, relations and source."
context: "M1 model instance"
scope: "Concrete requirements, entities, rules, flows, interfaces, errors, tasks and code artifacts"
allowed_synonyms:
  - "element instance"
forbidden_synonyms:
  - "word"
  - "label"
  - "shape"
not_examples:
  - "unnamed diagram box"
  - "free text mention"
related_element_types:
  - TYPE-MODEL
related_relation_types:
  - REL-CONTAINS
  - REL-REFERENCES
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "Structured Facts"
  - "Model Registers"
open_questions: []
```

### 8.5. Relation Type

```yaml
id: TERM-REL-001
term: Relation Type
status: candidate
definition: "A defined type of directed connection allowed between model elements."
context: "M2 metamodel definition"
scope: "Relations such as contains, validates, raises, triggers, provides, verifies"
allowed_synonyms:
  - "typed relation"
forbidden_synonyms:
  - "line"
  - "arrow"
  - "association without meaning"
not_examples:
  - "diagram arrow without source/target meaning"
related_element_types:
  - TYPE-DEPENDENCY
related_relation_types:
  - REL-CONFORMS-TO
source:
  - "docs/08_digital_system_cad/metamodel/02_Model_Relations.md"
used_in:
  - "Structured Facts"
open_questions: []
```

### 8.6. Structured Fact

```yaml
id: TERM-FACT-001
term: Structured Fact
status: candidate
definition: "A checkable statement about a digital system expressed as subject element, relation type and object element, with source and validation status."
context: "Digital System CAD model facts"
scope: "Model truth units used by registers, views, SDD, traceability and Codex context"
allowed_synonyms:
  - "model fact"
forbidden_synonyms:
  - "note"
  - "diagram arrow"
  - "free text claim"
not_examples:
  - "Entity mentioned in prose without relation"
related_element_types:
  - TYPE-MODEL
related_relation_types:
  - REL-REFERENCES
source:
  - "docs/08_digital_system_cad/metamodel/03_Structured_Facts.md"
used_in:
  - "Model Registers"
  - "Traceability"
  - "SDD From Model"
open_questions:
  - "Should facts be stored as YAML blocks, Markdown tables or separate files?"
```

## 9. View and transformation terms

### 9.1. View

```yaml
id: TERM-VIEW-001
term: View
status: candidate
definition: "A representation of selected model elements and structured facts for a particular purpose, audience and viewpoint."
context: "Model representation"
scope: "Diagrams, tables, forms, SDD sections, task lists, test plans and Codex context"
allowed_synonyms:
  - "representation"
forbidden_synonyms:
  - "source of truth"
  - "independent document"
not_examples:
  - "diagram that contains unmodeled meaning"
related_element_types:
  - TYPE-VIEW
related_relation_types:
  - REL-REPRESENTS
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "Model Registers"
  - "SDD From Model"
open_questions: []
```

### 9.2. Viewpoint

```yaml
id: TERM-VIEW-002
term: Viewpoint
status: candidate
definition: "A rule for constructing views that address specific stakeholder concerns."
context: "Architecture and model representation"
scope: "Requirements, architecture, data, behavior, testing, implementation and Codex-context viewpoints"
allowed_synonyms:
  - "view construction rule"
forbidden_synonyms:
  - "diagram style"
  - "audience only"
not_examples:
  - "random table filter"
related_element_types:
  - TYPE-VIEWPOINT
related_relation_types:
  - REL-CONFORMS-TO
source:
  - "docs/08_digital_system_cad/research/01_Metamodeling_Methods_And_Standards.md"
used_in:
  - "Model Elements"
  - "SDD From Model"
open_questions:
  - "What is the minimum viewpoint set for Digital System CAD?"
```

### 9.3. Transformation

```yaml
id: TERM-TR-001
term: Transformation
status: candidate
definition: "A rule-based conversion from model elements and structured facts into another view, document, task list, test plan, model or Codex context."
context: "Generation from model"
scope: "model -> SDD, model -> tasks, model -> tests, questionnaire answers -> model"
allowed_synonyms:
  - "model transformation"
forbidden_synonyms:
  - "random text generation"
  - "manual copy-paste"
not_examples:
  - "prompt that ignores structured facts"
related_element_types:
  - TYPE-TRANSFORMATION
related_relation_types:
  - REL-PRODUCES
  - REL-GENERATED-FROM
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "SDD From Model"
open_questions:
  - "How formal should transformations be in the Markdown prototype?"
```

### 9.4. Register

```yaml
id: TERM-VIEW-003
term: Register
status: candidate
definition: "A tabular view over model elements and structured facts."
context: "Model views"
scope: "Requirements register, entities register, facts register, traceability matrix"
allowed_synonyms:
  - "table view"
forbidden_synonyms:
  - "source of truth"
  - "database table"
not_examples:
  - "manual table with unmodeled facts"
related_element_types:
  - TYPE-VIEW
related_relation_types:
  - REL-REPRESENTS
source:
  - "docs/08_digital_system_cad/metamodel/04_Model_Registers.md"
used_in:
  - "Model Registers"
open_questions:
  - "Should first registers be Markdown tables or YAML/CSV?"
```

## 10. Core element terms

### 10.1. Entity

```yaml
id: TERM-ELEM-001
term: Entity
status: candidate
definition: "A modeled object that the system identifies, stores, processes, validates, transfers or produces as information."
context: "Logical system model"
scope: "Domain objects, system resources, information objects, runtime objects and result objects"
allowed_synonyms:
  - "model object"
forbidden_synonyms:
  - "variable"
  - "field"
  - "class"
  - "service"
not_examples:
  - "temporary value"
  - "UI label"
  - "FileScanner when it means an executor"
related_element_types:
  - TYPE-ENTITY
related_relation_types:
  - REL-CONTAINS
  - REL-BELONGS-TO
source:
  - "docs/05_encyclopedia/Entities.md"
used_in:
  - "Model Elements"
  - "Model Registers"
open_questions:
  - "Boundary between Entity, ValueObject, DTO, Record, ViewModel, SystemResource, InformationObject and RuntimeObject."
```

### 10.2. DataField

```yaml
id: TERM-ELEM-002
term: DataField
status: candidate
definition: "A typed value, parameter, signal, attribute or message part owned by another model element."
context: "Data model"
scope: "Fields owned by Entity, Interface, Event, Configuration or Storage"
allowed_synonyms:
  - "field"
  - "attribute"
  - "parameter"
forbidden_synonyms:
  - "entity"
  - "rule"
not_examples:
  - "whole document without structure"
related_element_types:
  - TYPE-DATAFIELD
related_relation_types:
  - REL-BELONGS-TO
  - REL-VALIDATES
source:
  - "docs/05_encyclopedia/Data.md"
used_in:
  - "Model Elements"
  - "Model Registers"
open_questions:
  - "Boundary between DataField, Parameter, Signal, Message and Document."
```

### 10.3. Rule

```yaml
id: TERM-ELEM-003
term: Rule
status: candidate
definition: "A checkable condition, constraint, calculation, transition guard, permission or reaction."
context: "Constraint model"
scope: "Validation rules, business rules, technical rules, transition rules and error rules"
allowed_synonyms:
  - "constraint"
forbidden_synonyms:
  - "code line"
  - "library"
  - "wish"
not_examples:
  - "system should work correctly"
related_element_types:
  - TYPE-RULE
related_relation_types:
  - REL-VALIDATES
  - REL-RAISES
  - REL-GUARDS
source:
  - "docs/05_encyclopedia/Rules.md"
used_in:
  - "Structured Facts"
open_questions:
  - "How to express rules declaratively in early docs?"
```

### 10.4. Error

```yaml
id: TERM-ELEM-004
term: Error
status: candidate
definition: "An invalid, exceptional, unsafe or unresolved condition and the required system reaction."
context: "Reliability and negative scenarios"
scope: "Invalid data, rule violations, integration failures, unsafe states and storage failures"
allowed_synonyms:
  - "failure condition"
forbidden_synonyms:
  - "traceback"
  - "open question"
not_examples:
  - "message without cause"
related_element_types:
  - TYPE-ERROR
related_relation_types:
  - REL-RAISES
source:
  - "docs/05_encyclopedia/Errors.md"
used_in:
  - "Model Registers"
  - "SDD From Model"
open_questions:
  - "Boundary between Error, Warning, Fault, Alarm, Exception and OpenQuestion."
```

### 10.5. Interface

```yaml
id: TERM-ELEM-005
term: Interface
status: candidate
definition: "A boundary of interaction with defined participants, input, output, commands, events, errors and contract."
context: "Boundary model"
scope: "UI, API, CLI, files, module contracts, hardware signals and test interfaces"
allowed_synonyms:
  - "interaction boundary"
forbidden_synonyms:
  - "screen only"
  - "button"
  - "module"
not_examples:
  - "endpoint without contract"
related_element_types:
  - TYPE-INTERFACE
related_relation_types:
  - REL-ACCEPTS
  - REL-RETURNS
  - REL-EXPOSES
source:
  - "docs/05_encyclopedia/Interfaces.md"
used_in:
  - "Model Elements"
  - "Model Registers"
open_questions:
  - "Boundary between Interface, Port, API, UI, Protocol, FileFormat and Connector."
```

## 11. Architecture terms

### 11.1. Module

```yaml
id: TERM-ARCH-001
term: Module
status: candidate
definition: "An architectural responsibility boundary that groups related services, rules, entities, interfaces or code artifacts."
context: "Architecture model"
scope: "Architecture responsibilities derived from logical model elements and flows"
allowed_synonyms:
  - "architectural module"
forbidden_synonyms:
  - "file"
  - "class"
  - "random function group"
  - "single operation"
not_examples:
  - "domain entity"
related_element_types:
  - TYPE-MODULE
related_relation_types:
  - REL-PROVIDES
  - REL-CONTAINS
  - REL-IMPLEMENTS
source:
  - "docs/05_encyclopedia/Modules.md"
used_in:
  - "Model Elements"
  - "Model Registers"
open_questions:
  - "Boundary between Module, Component, Service, Adapter, Layer and CodeArtifact."
```

### 11.2. Service

```yaml
id: TERM-ARCH-002
term: Service
status: candidate
definition: "A logical executor of an operation or behavior that acts on entities but is not itself the primary stored domain object."
context: "Behavior and architecture model"
scope: "Application services, domain services, infrastructure services, scanners, readers, writers, calculators, validators and coordinators"
allowed_synonyms:
  - "service"
  - "operation executor"
forbidden_synonyms:
  - "entity"
  - "module"
  - "code file"
  - "class by default"
not_examples:
  - "SourceFile"
  - "ScanJob"
  - "src/scanning/file_scanner.py"
related_element_types:
  - TYPE-SERVICE
related_relation_types:
  - REL-CONTAINS
  - REL-PROCESSES
  - REL-CREATES
  - REL-IS-IMPLEMENTED-BY
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "Model Elements"
  - "Model Registers"
  - "Traceability"
open_questions:
  - "Boundary between Service, Module, Adapter, UseCase and Function."
```

### 11.3. Dependency

```yaml
id: TERM-ARCH-003
term: Dependency
status: candidate
definition: "A typed directed relation showing that one element uses, requires, calls, reads, writes, implements or constrains another element."
context: "Architecture and model relations"
scope: "Module, layer, view, transformation, requirement and code dependencies"
allowed_synonyms:
  - "directed dependency"
forbidden_synonyms:
  - "visual proximity"
  - "association without direction"
not_examples:
  - "two blocks placed near each other"
related_element_types:
  - TYPE-DEPENDENCY
related_relation_types:
  - REL-DEPENDS-ON
source:
  - "docs/05_encyclopedia/Dependencies.md"
used_in:
  - "Model Relations"
open_questions:
  - "Should Dependency be an element type or only a relation family?"
```

### 11.4. CodeArtifact

```yaml
id: TERM-ARCH-004
term: CodeArtifact
status: candidate
definition: "A file, module, package, schema, configuration, test file or generated artifact that realizes part of the model or task."
context: "Implementation traceability"
scope: "Artifacts that can be traced back to tasks, modules, requirements, tests or transformations"
allowed_synonyms:
  - "implementation artifact"
forbidden_synonyms:
  - "model element without implementation"
  - "requirement"
not_examples:
  - "abstract module without file or artifact"
related_element_types:
  - TYPE-CODEARTIFACT
related_relation_types:
  - REL-IMPLEMENTS
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "Traceability"
open_questions:
  - "How to represent generated artifacts versus hand-written artifacts?"
```

## 12. Status terms

### 12.1. Candidate

```yaml
id: TERM-STATUS-001
term: candidate
status: candidate
definition: "A working model item that appears useful but has not yet been validated across enough examples."
context: "Element, relation, fact and term status"
scope: "Current research stage"
allowed_synonyms:
  - "working candidate"
forbidden_synonyms:
  - "final"
  - "proven"
not_examples:
  - "accepted universal kernel element"
related_element_types:
  - TYPE-MODEL
related_relation_types: []
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "Model Elements"
  - "Model Relations"
open_questions: []
```

### 12.2. Accepted

```yaml
id: TERM-STATUS-002
term: accepted
status: candidate
definition: "A model item accepted for the current model version after validation or explicit decision."
context: "Element, relation, fact and term status"
scope: "Current model version"
allowed_synonyms:
  - "approved"
forbidden_synonyms:
  - "universal forever"
not_examples:
  - "candidate not yet checked"
related_element_types:
  - TYPE-MODEL
related_relation_types: []
source:
  - "docs/08_digital_system_cad/metamodel/03_Structured_Facts.md"
used_in:
  - "Structured Facts"
open_questions:
  - "Who or what accepts a model item in early research?"
```

### 12.3. OpenQuestion

```yaml
id: TERM-STATUS-003
term: OpenQuestion
status: candidate
definition: "An explicit unresolved uncertainty that must not be silently converted into a model fact."
context: "Model governance"
scope: "Unclear boundaries, missing sources, ambiguous element types, relation uncertainty and validation gaps"
allowed_synonyms:
  - "open question"
  - "unresolved question"
forbidden_synonyms:
  - "error"
  - "assumption"
  - "TODO without context"
not_examples:
  - "known defect with defined reaction"
related_element_types:
  - TYPE-OPEN-QUESTION
related_relation_types:
  - REL-AFFECTS
  - REL-RESOLVES
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
used_in:
  - "Model Registers"
  - "Traceability"
open_questions:
  - "Should Decision be a separate element type?"
```

### 12.4. RequirementGap

```yaml
id: TERM-REQ-GAP-001
term: RequirementGap
status: candidate
definition: "Разрыв требований: нужна проверка, но нет ясного Requirement, который задаёт ожидаемое поведение системы."
context: "Requirements, verification and traceability"
scope: "Missing, unclear or incomplete requirement discovered through TestCase, ValidationRule, Review or SDD completeness check"
allowed_synonyms:
  - "requirement gap"
  - "gap in requirements"
  - "missing requirement"
forbidden_synonyms:
  - "test requirement"
  - "failed test"
  - "bug"
  - "ordinary TODO"
not_examples:
  - "TestCase failed against a clear Requirement"
  - "implementation defect"
  - "unclear term not connected to verification"
related_element_types:
  - TYPE-REQUIREMENT-GAP
  - TYPE-REQUIREMENT
  - TYPE-TESTCASE
related_relation_types:
  - REL-REVEALS-GAP
  - REL-BLOCKED-BY
  - REL-AFFECTS
  - REL-RESOLVES
source:
  - "docs/08_digital_system_cad/metamodel/01_Model_Elements.md"
  - "docs/08_digital_system_cad/metamodel/06_Traceability.md"
used_in:
  - "Requirements Register"
  - "TestCases Register"
  - "OpenQuestions Register"
  - "Traceability"
open_questions:
  - "Should RequirementGap remain separate from OpenQuestion or become an OpenQuestion subtype?"
```

### 12.5. pending_requirement

```yaml
id: TERM-STATUS-004
term: pending_requirement
status: candidate
definition: "Статус TestCase, Task или SDD section, показывающий, что работа ожидает создания или уточнения Requirement."
context: "Verification workflow and traceability status"
scope: "Items blocked by RequirementGap"
allowed_synonyms:
  - "blocked by requirement gap"
forbidden_synonyms:
  - "ready"
  - "verified"
  - "implemented"
not_examples:
  - "test waiting for code implementation while Requirement is clear"
related_element_types:
  - TYPE-TESTCASE
  - TYPE-REQUIREMENT-GAP
related_relation_types:
  - REL-BLOCKED-BY
source:
  - "docs/08_digital_system_cad/metamodel/06_Traceability.md"
used_in:
  - "TestCases Register"
  - "Traceability Matrix"
open_questions: []
```

## 13. Forbidden ambiguous terms

Эти слова нельзя использовать как точные термины без уточнения:

| Term | Почему опасен | Что делать |
|---|---|---|
| object | может означать Entity, object in code, data object, UI object | заменить на точный element type |
| model | может означать model, data model, ML model, class model | указать контекст |
| relation | может означать DB relation, UML association, typed relation | использовать Relation Type или structured fact |
| view | может означать UI view, database view, model view | указать viewpoint и source elements |
| module | может означать Python file, package, architectural responsibility | уточнить Module или CodeArtifact |
| data | слишком широкое слово | уточнить DataField, DataStructure, Message, Document |
| process | может означать Flow, Scenario, runtime process, business process | уточнить element type |
| state | может означать status, mode, phase, error state | указать owner и behavior impact |
| interface | может означать UI, API, hardware, module contract | указать kind и contract |
| error | может означать exception, fault, alarm, warning | указать severity, cause and reaction |

Если термин из списка нужен, но точный смысл не выбран, нужно создать OpenQuestion.

## 14. Rules for adding terms

### 14.1. TERM-VAL-001. Term must have definition

Нельзя добавлять важный термин без `definition`.

Severity: `blocker`

### 14.2. TERM-VAL-002. Term must have context

Нельзя использовать термин без указания контекста, если он может иметь разные смыслы.

Severity: `error`

### 14.3. TERM-VAL-003. Name is not definition

Повторение имени другими словами не является определением.

Bad:

```text
Entity is an entity.
```

Good:

```text
Entity is a significant object or concept with stable identity, definition, purpose and relations.
```

Severity: `error`

### 14.4. TERM-VAL-004. Forbidden synonym must not be used as exact term

Если слово находится в `forbidden_synonyms`, его нельзя использовать как точный термин без уточнения.

Severity: `warning`

### 14.5. TERM-VAL-005. New concept must link to model

Новый термин должен быть связан хотя бы с одним:

- element type;
- relation type;
- field;
- view;
- transformation;
- validation rule;
- domain profile;
- open question.

Severity: `warning`

### 14.6. TERM-VAL-006. Ambiguity creates OpenQuestion

Если термин нельзя определить достаточно точно, нужно создать OpenQuestion вместо догадки.

Severity: `error`

## 15. Vocabulary and SDD

Controlled vocabulary должен питать:

- glossary section;
- SDD definitions;
- naming policy;
- requirements wording;
- error wording;
- interface contract wording;
- Codex prompt context.

Если SDD использует термин, которого нет в vocabulary, нужно:

1. добавить термин;
2. дать definition;
3. указать context;
4. указать source;
5. связать с element type или relation type;
6. зафиксировать OpenQuestion, если термин неясен.

## 16. Vocabulary and Codex context

Codex context должен получать не только задачу, но и словарь:

```yaml
terms:
  Entity:
    definition: "A significant object or concept with stable identity, definition, purpose and relations."
    forbidden_synonyms:
      - "variable"
      - "field"
  View:
    definition: "A representation of selected model elements and structured facts."
    warning: "View is not source of truth."
```

Это снижает риск, что Codex:

- превратит diagram в source of truth;
- назовёт файл модулем без архитектурной ответственности;
- примет field за Entity;
- создаст SDD из свободного текста без facts.

## 17. Минимальный vocabulary для первого validation example

Для первого примера нужно стабилизировать минимум:

- Project;
- Requirement;
- Entity;
- DataField;
- Rule;
- Error;
- Event;
- Flow;
- Storage;
- Interface;
- Module;
- TestCase;
- Task;
- CodeArtifact;
- Structured Fact;
- Register;
- View;
- SDD;
- OpenQuestion.

Если пример вводит доменный термин, например `InputFile`, `Report`, `Parser`, `Material`, `Tool`, он должен получить либо:

- domain-specific term entry;
- Entity entry;
- DataField entry;
- Module entry;
- OpenQuestion о классификации.

## 18. Открытые вопросы

- Должен ли vocabulary быть одним файлом или набором файлов по областям?
- Нужно ли хранить terms как YAML-блоки, Markdown-таблицы или отдельные карточки?
- Нужно ли добавлять multilingual terms: English / Russian?
- Как контролировать терминологию в уже существующих документах?
- Какие термины считать accepted после первой проверки?
- Нужно ли вводить `Decision` как отдельный type для утверждения терминов?

## 19. Связанные документы

### Входные документы

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Передаёт: element types и definitions.
  - Используется для: core vocabulary.
  - Ограничение: не фиксирует синонимы и forbidden terms подробно.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Передаёт: relation types.
  - Используется для: vocabulary relation names.
  - Ограничение: не описывает general terminology policy.

- [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
  - Передаёт: term Structured Fact and fact validation needs.
  - Используется для: vocabulary around facts, source and validation.
  - Ограничение: не стабилизирует весь glossary.

- [[docs/08_digital_system_cad/metamodel/04_Model_Registers|Model Registers]]
  - Передаёт: register, ID, status and field terms.
  - Используется для: vocabulary of tabular views.
  - Ограничение: не описывает term governance.

### Выходные документы

- Будущий [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Получает: стабильные термины для цепочек трассировки.
  - Используется для: минимизации неоднозначности между Requirement, Task, CodeArtifact и TestCase.
  - Ограничение: не должен становиться glossary.

- Будущий [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]
  - Получает: правила терминов и SDD glossary.
  - Используется для: генерации SDD без терминологических конфликтов.
  - Ограничение: не должен менять vocabulary без обратной правки.

## 20. История изменений

- Initial version: создан controlled vocabulary для Digital System CAD с формой term, статусами, core modeling terms, view/transformation terms, core element terms, architecture terms, forbidden ambiguous terms и validation rules.
