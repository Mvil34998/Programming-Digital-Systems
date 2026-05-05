# SDD From Model

## 1. Назначение документа

`07_SDD_From_Model.md` описывает, как SDD должен формироваться из модели Digital System CAD.

SDD здесь рассматривается не как свободный документ, а как набор views и transformations над model elements, structured facts, registers, controlled vocabulary и traceability rules.

> [!info] Главное
> SDD не должен быть отдельным источником истины. Источник истины — модель: typed elements, typed relations, structured facts, validation rules и traceability.

## 2. Базовая формула

```text
Model -> Views -> SDD sections
Model -> Transformations -> SDD documents
```

Расширенная формула:

```text
Element Types
+ Relation Types
+ Structured Facts
+ Registers
+ Controlled Vocabulary
+ Traceability Rules
+ Validation Rules
= SDD source model
```

SDD section:

```text
SDD section = selected facts + selected fields + viewpoint + transformation rule + validation status
```

## 3. Что SDD должен делать

SDD должен:

- объяснять систему человеку;
- давать Codex структурированный контекст;
- показывать requirements;
- показывать model elements;
- показывать rules, errors, flows and interfaces;
- показывать architecture decisions;
- показывать traceability;
- показывать open questions;
- помогать формировать tasks and tests.

SDD не должен:

- вводить новые факты без записи в модель;
- дублировать registers как самостоятельный источник правды;
- скрывать open questions;
- подменять validation;
- превращать архитектурные предположения в решения без source.

## 4. SDD document set

Минимальный набор SDD-документов:

```text
spec.md
requirements.md
glossary.md
model-overview.md
entities.md
data-model.md
rules.md
states.md
events.md
flows.md
storage.md
interfaces.md
integrations.md
errors.md
architecture.md
tests.md
traceability.md
open-questions.md
plan.md
tasks.md
```

Для маленького проекта не обязательно создавать все файлы физически. Но модель должна позволять понять, какие sections нужны и какие можно пропустить.

## 5. Universal SDD section form

```yaml
id:
title:
purpose:
viewpoint:
audience:
source_elements:
source_facts:
source_registers:
transformation_rule:
required_validation:
content_outline:
generated_from:
manual_notes:
open_questions:
```

Правила:

- `source_elements` должны ссылаться на Model Elements;
- `source_facts` должны ссылаться на Structured Facts;
- `source_registers` должны быть views, а не source of truth;
- `generated_from` должен показывать происхождение;
- `manual_notes` не должны вводить новый смысл без facts;
- `open_questions` должны быть видимыми.

## 6. SDD sections mapping

### 6.1. `spec.md`

Назначение: верхнее описание системы.

Source:

- Project;
- top-level Requirements;
- Scope facts;
- OpenQuestions;
- Controlled Vocabulary.

Required facts:

```text
Project contains Requirement
Project sourced_from SourceDocument
Project has OpenQuestion
```

Validation before generation:

- Project has definition;
- Project has scope;
- Project has source;
- key terms exist in Controlled Vocabulary.

### 6.2. `requirements.md`

Назначение: требования и критерии проверки.

Source:

- Requirements Register;
- TestCases Register;
- Traceability Matrix.

Required facts:

```text
Project contains Requirement
Requirement is_verified_by TestCase
Requirement references ModelElement
```

Validation before generation:

- every Requirement has source;
- every Requirement has verification or OpenQuestion/RequirementGap;
- vague requirements are marked as gaps.

### 6.3. `glossary.md`

Назначение: стабилизировать термины SDD.

Source:

- Controlled Vocabulary.

Required facts:

```text
Term related_to ElementType
Term used_in SDDSection
```

Validation before generation:

- every important SDD term has definition;
- forbidden synonyms are not used as exact terms;
- ambiguous terms have OpenQuestion.

### 6.4. `model-overview.md`

Назначение: показать состав модели и основные views.

Source:

- Model;
- Model Elements;
- Model Relations;
- Structured Facts;
- Registers.

Required facts:

```text
Model contains ModelElement
Model contains StructuredFact
View represents ModelElement
```

Validation before generation:

- Model has element types;
- Model has relation types;
- facts have subject/relation/object.

### 6.5. `entities.md`

Назначение: описать сущности.

Source:

- Entities Register;
- DataFields Register;
- Facts Register.

Required facts:

```text
Entity contains DataField
Entity has State
Entity participates_in Flow
Storage stores Entity
```

Validation before generation:

- Entity has definition;
- Entity has source;
- critical Entity has related DataField or OpenQuestion.

### 6.6. `data-model.md`

Назначение: описать данные, поля, форматы, владельцев и проверки.

Source:

- DataFields Register;
- Rules Register;
- Storage Register;
- Interfaces Register.

Required facts:

```text
DataField belongs_to Entity / Interface / Event / Configuration
Rule validates DataField
Storage stores DataField
Interface accepts DataField
```

Validation before generation:

- DataField has owner;
- critical DataField has validation rule;
- invalid data behavior is known or marked as OpenQuestion.

### 6.7. `rules.md`

Назначение: описать правила и последствия нарушения.

Source:

- Rules Register;
- Errors Register;
- TestCases Register.

Required facts:

```text
Rule validates DataField
Rule constrains Entity / Flow / Interface / State
Rule raises Error
TestCase verifies Rule
```

Validation before generation:

- Rule has condition;
- Rule has expected result;
- critical Rule has violation behavior;
- critical Rule has TestCase or OpenQuestion.

### 6.8. `states.md`

Назначение: описать состояния и переходы.

Source:

- States Register;
- Events Register;
- Rules Register.

Required facts:

```text
State belongs_to owner
Event triggers StateTransition
Rule guards StateTransition
```

Validation before generation:

- State has owner;
- State has behavior impact;
- transitions are explicit or marked as OpenQuestion.

### 6.9. `events.md`

Назначение: описать события, источники и реакции.

Source:

- Events Register;
- Flows Register;
- Rules Register;
- Errors Register.

Required facts:

```text
Event triggers Flow
Event carries DataField
Rule handles Event
Event may_raise Error
```

Validation before generation:

- Event has source;
- Event has reaction;
- allowed states are known or marked as OpenQuestion.

### 6.10. `flows.md`

Назначение: описать движение данных, команд, событий, ошибок и результатов.

Source:

- Flows Register;
- Events Register;
- DataFields Register;
- Errors Register.

Required facts:

```text
Event triggers Flow
Flow transfers DataField / Entity / Event
Rule guards Flow
Flow may_raise Error
```

Validation before generation:

- Flow has source;
- Flow has target;
- Flow has transferred object;
- critical Flow has error behavior.

### 6.11. `storage.md`

Назначение: описать хранимые данные, жизненный цикл, целостность и ошибки.

Source:

- Storage Register;
- DataFields Register;
- Entities Register;
- Errors Register.

Required facts:

```text
Storage stores Entity / DataField / Event / State / Configuration
Flow reads_from Storage
Flow writes_to Storage
Error occurs_in Storage
```

Validation before generation:

- Storage has stored elements;
- Storage has purpose;
- integrity rules are known or marked as OpenQuestion.

### 6.12. `interfaces.md`

Назначение: описать интерфейсы и контракты взаимодействия.

Source:

- Interfaces Register;
- DataFields Register;
- Events Register;
- Errors Register.

Required facts:

```text
Interface accepts DataField / Event / Command
Interface returns DataField / Error
Interface exposes Entity
Module provides Interface
```

Validation before generation:

- Interface has participants;
- Interface has input/output or reason;
- Interface errors are explicit.

### 6.13. `integrations.md`

Назначение: описать внешние системы и обмен.

Source:

- Integrations Register;
- Interfaces Register;
- Flows Register;
- Errors Register.

Required facts:

```text
Integration uses Interface
Integration exchanges_with ExternalSystem
Integration exchanges DataField / Event
Integration may_raise Error
```

Validation before generation:

- external boundary is clear;
- exchanged data is defined;
- failure behavior is defined.

### 6.14. `errors.md`

Назначение: описать ошибки, причины, критичность и реакцию.

Source:

- Errors Register;
- Rules Register;
- Flows Register;
- TestCases Register.

Required facts:

```text
Error caused_by Rule / DataField / State / Flow / Storage / Interface
Flow handles Error
Interface returns Error
TestCase verifies Error
```

Validation before generation:

- Error has cause;
- Error has severity;
- Error has reaction;
- critical Error has TestCase or OpenQuestion.

### 6.15. `architecture.md`

Назначение: описать архитектурные элементы, границы и зависимости.

Source:

- Layers Register;
- Modules Register;
- Services Register;
- Interfaces Register;
- Dependencies Register;
- Traceability Matrix.

Required facts:

```text
Layer contains Module
Module contains Service
Module provides Interface
Service processes Entity
Service creates Entity
Service is_implemented_by CodeArtifact
Module executes Flow
Module implements Rule
Module depends_on Module
```

Validation before generation:

- Module has responsibility;
- Service has operation and owner Module;
- dependencies have direction and reason;
- architectural choices have source or OpenQuestion.

### 6.16. `tests.md`

Назначение: описать проверку требований, правил, ошибок, потоков и кода.

Source:

- TestCases Register;
- Requirements Register;
- Rules Register;
- Errors Register;
- Traceability Matrix.

Required facts:

```text
TestCase verifies Requirement
TestCase verifies Rule
TestCase verifies Error
TestCase verifies CodeArtifact
TestCase reveals_gap RequirementGap
TestCase blocked_by RequirementGap
```

Validation before generation:

- TestCase has target;
- TestCase has expected result;
- critical requirements and errors are covered.
- TestCase without clear Requirement is shown as `pending_requirement`, not as verified behavior.
- RequirementGap must appear in open questions / gaps until Requirement is created or updated.

### 6.17. `traceability.md`

Назначение: показать цепочки трассировки и gaps.

Source:

- Traceability Matrix;
- Facts Register;
- OpenQuestions Register.

Required facts:

```text
Requirement is_verified_by TestCase
Task implements Requirement
Task updates CodeArtifact
Module contains Service
Service is_implemented_by CodeArtifact
CodeArtifact implements Service / Module
```

Validation before generation:

- gaps are explicit;
- required chains are checked;
- unresolved gaps have OpenQuestion or RequirementGap.

### 6.18. `open-questions.md`

Назначение: показать нерешённые вопросы.

Source:

- OpenQuestions Register;
- Facts Register.

Required facts:

```text
OpenQuestion affects ModelElement / Relation / View / Transformation
Task resolves OpenQuestion
RequirementGap affects Requirement / TestCase / SDDSection
Requirement resolves RequirementGap
```

Validation before generation:

- OpenQuestion has context;
- OpenQuestion affects something;
- resolved questions have resolution source.
- RequirementGap has linked needed check and resolution path.

### 6.19. `plan.md`

Назначение: описать план движения от модели к реализации.

Source:

- Requirements Register;
- Traceability Matrix;
- Tasks Register;
- OpenQuestions Register.

Required facts:

```text
Task implements Requirement
Task resolves OpenQuestion
Task updates ModelElement
```

Validation before generation:

- tasks have source;
- tasks have expected output;
- blockers are visible.

### 6.20. `tasks.md`

Назначение: дать Codex и разработчику исполнимые задачи.

Source:

- Tasks Register;
- CodeArtifacts Register;
- TestCases Register;
- Traceability Matrix.

Required facts:

```text
Task implements Requirement
Task changes CodeArtifact
TestCase verifies Task / CodeArtifact
```

Validation before generation:

- Task has expected output;
- Task has affected elements;
- Task has verification path or OpenQuestion.

## 7. SDD transformation form

```yaml
transformation:
  id:
  name:
  input_elements:
  input_facts:
  input_registers:
  input_vocabulary:
  output_section:
  viewpoint:
  rules:
  validation_before:
  validation_after:
  gaps:
  open_questions:
```

Example:

```yaml
transformation:
  id: TR-SDD-RULES-001
  name: "Rules section from model"
  input_elements:
    - TYPE-RULE
    - TYPE-DATAFIELD
    - TYPE-ERROR
    - TYPE-TESTCASE
  input_facts:
    - "Rule validates DataField"
    - "Rule raises Error"
    - "TestCase verifies Rule"
  input_registers:
    - Rules Register
    - Errors Register
    - TestCases Register
  output_section: rules.md
  viewpoint: requirements/testing viewpoint
  validation_before:
    - "Rule has condition"
    - "Rule has violation behavior"
  validation_after:
    - "Every critical Rule appears in rules.md"
  gaps:
    - "critical Rule without TestCase"
  open_questions: []
```

## 8. SDD generation validation

### 8.1. SDD-VAL-001. Section must have source model

Каждый SDD section должен ссылаться на source elements или source facts.

Severity: `error`

### 8.2. SDD-VAL-002. Section must have viewpoint

Каждый SDD section должен иметь viewpoint или documented reason.

Severity: `warning`

### 8.3. SDD-VAL-003. Manual claim must become fact

Если SDD section содержит новый смысл, которого нет в model facts, нужно создать fact или OpenQuestion.

Severity: `warning`

### 8.4. SDD-VAL-004. Critical gaps must be visible

SDD не должен скрывать gaps, влияющие на требования, правила, ошибки, тесты и задачи.

Severity: `error`

### 8.5. SDD-VAL-005. SDD terms must exist in vocabulary

Важные термины SDD должны иметь entry в Controlled Vocabulary.

Severity: `warning`

### 8.6. SDD-VAL-006. SDD traceability must be available

Sections `requirements.md`, `tests.md`, `tasks.md` и `traceability.md` должны иметь traceability facts.

Severity: `error`

## 9. SDD and Codex context

Codex context может быть SDD-derived view:

```yaml
codex_context:
  task: TASK-001
  relevant_sdd_sections:
    - requirements.md
    - rules.md
    - interfaces.md
    - tests.md
  source_facts:
    - FACT-REQ-001
    - FACT-RULE-001
    - FACT-INT-001
  must_preserve:
    - RULE-001
    - INTERFACE-001
  validation:
    - TEST-001
  open_questions:
    - OQ-001
```

Codex должен получать не только prose, но и IDs, facts, constraints and tests.

## 10. First SDD validation example

Первый пример:

- [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]]

Минимальный SDD для проверки:

```text
spec.md
requirements.md
entities.md
data-model.md
rules.md
errors.md
flows.md
interfaces.md
tests.md
tasks.md
traceability.md
open-questions.md
```

Порядок проверки:

1. Выделить Requirements.
2. Выделить Entities и DataFields.
3. Выделить Rules и Errors.
4. Выделить Flows и Interfaces.
5. Создать TestCases.
6. Создать Tasks.
7. Собрать минимальные SDD sections.
8. Проверить gaps.
9. Зафиксировать, какие element types были полезны.
10. Зафиксировать, какие element types оказались лишними.

## 11. Открытые вопросы

- Должен ли SDD физически храниться в одной папке на проект или генерироваться как временный view?
- Какие SDD sections обязательны для маленькой утилиты?
- Нужно ли вводить `SDDSection` как отдельный element type?
- Как фиксировать ручные правки сгенерированного SDD?
- Какой формат лучше для первого SDD: Markdown files, one Markdown document, or Obsidian folder?
- Какие validation rules являются blocker перед задачами Codex?

## 12. Связанные документы

### Входные документы

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Передаёт: element types, попадающие в SDD sections.
  - Используется для: mapping model -> SDD.
  - Ограничение: не описывает SDD transformations.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Передаёт: relation types, которые становятся traceability and section facts.
  - Используется для: required facts per section.
  - Ограничение: не описывает SDD section content.

- [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
  - Передаёт: facts as source of SDD truth.
  - Используется для: source_facts и generated_from.
  - Ограничение: не задаёт SDD document set.

- [[docs/08_digital_system_cad/metamodel/04_Model_Registers|Model Registers]]
  - Передаёт: register views.
  - Используется для: SDD tables and coverage matrices.
  - Ограничение: registers are not source of truth.

- [[docs/08_digital_system_cad/metamodel/05_Controlled_Vocabulary|Controlled Vocabulary]]
  - Передаёт: term definitions and forbidden synonyms.
  - Используется для: SDD glossary and wording.
  - Ограничение: не задаёт transformations.

- [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Передаёт: required chains and gaps.
  - Используется для: traceability.md and generation validation.
  - Ограничение: не задаёт весь SDD document set.

### Выходные документы

- Будущие validation examples.
  - Получают: SDD mapping rules.
  - Используются для: проверки, можно ли собрать SDD из модели.
  - Ограничение: не должны доказывать универсальность на одном примере.

## 13. История изменений

- Initial version: создана спецификация SDD as view/transformation модели Digital System CAD с document set, section mapping, transformation form, validation rules, Codex context and first validation example plan.
