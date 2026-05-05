# Model Relations

## 1. Назначение документа

`02_Model_Relations.md` описывает кандидаты типов связей для рабочей метамодели Digital System CAD.

Связь в Digital System CAD является объектом модели первого класса. Она не должна существовать только как линия на диаграмме, случайная фраза в тексте или неявная зависимость в коде.

> [!info] Главное
> Модель цифровой системы должна быть сетью typed elements и typed relations. Без связей список элементов остаётся словарём, а не моделью.

## 2. Основание

Документ опирается на:

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
- [[Digital_System_CAD_Philosophical_Essay_for_Codex|Digital System CAD Philosophical Essay]]
- [[docs/05_encyclopedia/Dependencies|Dependencies]]
- [[docs/05_encyclopedia/Architecture|Architecture]]

## 3. Универсальная форма Relation Type

Каждый тип связи должен описываться по форме:

```text
Relation ID:
Relation name:
Status:
Source type:
Target type:
Meaning:
Definition:
Required:
Cardinality:
Validation rule:
Examples:
Not examples:
Open questions:
```

Каждая конкретная связь M1 должна описываться по форме:

```text
ID:
Source element:
Relation:
Target element:
Meaning:
Reason:
Source:
Required:
Validation status:
Open questions:
```

## 4. Классификация связей

| Группа | Назначение |
|---|---|
| Containment | Показывает состав или владение |
| Description | Показывает, что один элемент описывает другой |
| Constraint | Показывает правила, ограничения и проверки |
| Behavior | Показывает события, состояния, потоки и реакции |
| Persistence | Показывает сохранение, чтение, запись и журналы |
| Boundary | Показывает интерфейсы, обмен и интеграции |
| Architecture | Показывает слои, модули, зависимости и реализацию |
| Verification | Показывает требования, тесты и критерии проверки |
| Transformation | Показывает views, viewpoints, generators и outputs |
| Governance | Показывает открытые вопросы, решения и источники |

## 5. Containment relations

### 5.1. contains

```text
Relation ID: REL-CONTAINS
Relation name: contains
Status: candidate
Source type: Project, Model, Layer, Module, Entity, Scenario, View
Target type: any compatible model element
Meaning: Source includes target as a meaningful part of its structure.
Definition: A containment relation states that the target belongs to the source for organization, scope or composition.
Required: conditional
Cardinality: one-to-many
Validation rule: Target should not be contained by multiple incompatible parents unless multi-containment is explicitly allowed.
Examples: Project contains Requirement; Entity contains DataField; Layer contains Module; Module contains Service.
Not examples: thematic similarity, visual grouping on a diagram.
Open questions: Which element types allow multiple containers?
```

### 5.2. belongs_to

```text
Relation ID: REL-BELONGS-TO
Relation name: belongs_to
Status: candidate
Source type: DataField, State, Event, Module, Configuration
Target type: Entity, Interface, Event, Layer, Project, Storage
Meaning: Source has an owner or parent context.
Definition: A belongs_to relation identifies the primary owner or context that gives meaning to the source element.
Required: yes for DataField, State and Event.
Cardinality: many-to-one
Validation rule: DataField without owner is incomplete.
Examples: DataField belongs_to Entity; Module belongs_to Layer.
Not examples: dependency, usage, similarity.
Open questions: Should belongs_to be replaced by specific relations for each source type?
```

## 6. Description relations

### 6.1. defines

```text
Relation ID: REL-DEFINES
Relation name: defines
Status: candidate
Source type: Requirement, Rule, Viewpoint, Metamodel, ControlledVocabulary
Target type: ModelElement, RelationType, View, ValidationRule
Meaning: Source gives formal meaning, constraint or scope to target.
Definition: A defines relation states that the target obtains its required meaning from the source.
Required: conditional
Cardinality: many-to-many
Validation rule: If source defines target, target should reference source as source of meaning.
Examples: Requirement defines Rule; Viewpoint defines View.
Not examples: implementation, verification.
Open questions: Should Definition itself be represented as a separate element?
```

### 6.2. references

```text
Relation ID: REL-REFERENCES
Relation name: references
Status: candidate
Source type: Requirement, Rule, View, DocumentSection, OpenQuestion
Target type: any model element
Meaning: Source mentions or depends on target for meaning without ownership.
Definition: A references relation preserves traceability from text or view to model element.
Required: conditional
Cardinality: many-to-many
Validation rule: Important references in SDD should point to stable IDs, not only names.
Examples: Requirement references Entity; View references Rule.
Not examples: contains, implements.
Open questions: How strict should reference extraction be in Markdown?
```

## 7. Constraint relations

### 7.1. validates

```text
Relation ID: REL-VALIDATES
Relation name: validates
Status: candidate
Source type: Rule, ValidationRule
Target type: DataField, Entity, Interface, Configuration, Model, StructuredFact
Meaning: Source checks whether target satisfies a condition.
Definition: A validates relation connects a checkable rule with the element it evaluates.
Required: yes for validation rules.
Cardinality: many-to-many
Validation rule: Rule that validates something must define condition, expected result and violation behavior.
Examples: Rule validates DataField; ValidationRule validates Model.
Not examples: TestCase verifies Rule.
Open questions: How to distinguish validation from verification in early docs?
```

### 7.2. constrains

```text
Relation ID: REL-CONSTRAINS
Relation name: constrains
Status: candidate
Source type: Rule, Requirement, Decision
Target type: Entity, State, Flow, Interface, Module, Layer, Transformation
Meaning: Source limits allowed structure or behavior of target.
Definition: A constrains relation states that target must obey source.
Required: conditional
Cardinality: many-to-many
Validation rule: Constraint should be checkable or have OpenQuestion.
Examples: Rule constrains Flow; Requirement constrains Interface.
Not examples: data ownership, event trigger.
Open questions: Should architectural constraints be a specialized relation?
```

### 7.3. raises

```text
Relation ID: REL-RAISES
Relation name: raises
Status: candidate
Source type: Rule, Flow, Interface, Storage, Integration, Module
Target type: Error
Meaning: Source can cause or report target error.
Definition: A raises relation connects a violation or failure point to an explicit Error.
Required: yes for critical rules and interfaces with negative scenarios.
Cardinality: many-to-many
Validation rule: Error must define cause, severity and reaction.
Examples: Rule raises Error; Interface returns Error; Storage raises Error.
Not examples: OpenQuestion, warning without reaction.
Open questions: Should Warning use same relation or separate relation?
```

### 7.4. guards

```text
Relation ID: REL-GUARDS
Relation name: guards
Status: candidate
Source type: Rule
Target type: StateTransition, Flow, Event, Interface command
Meaning: Source determines whether target may occur.
Definition: A guards relation attaches a condition to behavior.
Required: conditional
Cardinality: many-to-many
Validation rule: Guard must have clear condition and forbidden behavior.
Examples: Rule guards StateTransition; Rule guards Flow.
Not examples: Rule validates DataField.
Open questions: Should StateTransition become a separate element type?
```

## 8. Behavior relations

### 8.1. triggers

```text
Relation ID: REL-TRIGGERS
Relation name: triggers
Status: candidate
Source type: Event, Rule, Scenario
Target type: Flow, StateTransition, Transformation, Task
Meaning: Source starts target behavior.
Definition: A triggers relation identifies the cause that initiates an action, route or transformation.
Required: yes for Flow unless trigger is intentionally external/unknown.
Cardinality: one-to-many
Validation rule: Triggered target should have preconditions and result.
Examples: Event triggers Flow; Event triggers StateTransition.
Not examples: Dependency without temporal cause.
Open questions: Can Requirement trigger Task or should it only defines/splits_to Task?
```

### 8.2. changes_state_of

```text
Relation ID: REL-CHANGES-STATE-OF
Relation name: changes_state_of
Status: candidate
Source type: Event, Flow, Rule
Target type: Entity, Interface, Process, System, DataField
Meaning: Source causes a state change in target.
Definition: A changes_state_of relation connects a cause to the element whose State changes.
Required: conditional
Cardinality: many-to-many
Validation rule: Target should have known source and target states or an OpenQuestion.
Examples: Event changes_state_of Entity; Flow changes_state_of Process.
Not examples: Status field with no behavioral meaning.
Open questions: Should relation point to StateTransition instead of target element?
```

### 8.3. participates_in

```text
Relation ID: REL-PARTICIPATES-IN
Relation name: participates_in
Status: candidate
Source type: Actor, Entity, Interface, Module, ExternalSystem
Target type: Scenario, Flow, Integration
Meaning: Source is an active participant in target behavior.
Definition: A participates_in relation shows that source plays a role in a scenario, flow or integration.
Required: conditional
Cardinality: many-to-many
Validation rule: Participant role should be clear.
Examples: Actor participates_in Scenario; Entity participates_in Flow.
Not examples: passive reference in a note.
Open questions: Do we need role labels on this relation?
```

### 8.4. carries

```text
Relation ID: REL-CARRIES
Relation name: carries
Status: candidate
Source type: Event, Message, Flow, Interface
Target type: DataField, Entity
Meaning: Source transports or includes target as payload.
Definition: A carries relation states what data or entity moves with a behavior or exchange.
Required: conditional
Cardinality: many-to-many
Validation rule: Carried DataField should have type and owner.
Examples: Event carries DataField; Flow carries Entity.
Not examples: contains as structural ownership.
Open questions: Should transferred_object in Flow be modeled only through carries?
```

## 9. Persistence relations

### 9.1. stores

```text
Relation ID: REL-STORES
Relation name: stores
Status: candidate
Source type: Storage
Target type: Entity, DataField, Event, State, Configuration, Result
Meaning: Source persists target for later use.
Definition: A stores relation identifies what must be retained and managed by a storage element.
Required: yes for Storage.
Cardinality: one-to-many
Validation rule: Stored target should have purpose, lifecycle and integrity rules.
Examples: Storage stores Entity; Storage stores Event.
Not examples: temporary variable.
Open questions: Should log records be Event or separate LogEntry type?
```

### 9.2. reads_from

```text
Relation ID: REL-READS-FROM
Relation name: reads_from
Status: candidate
Source type: Flow, Module, Interface, Transformation
Target type: Storage, Model, Register, File, ExternalSystem
Meaning: Source obtains data from target.
Definition: A reads_from relation identifies source of data access.
Required: conditional
Cardinality: many-to-many
Validation rule: Read dependency should be explicit in architecture-sensitive flows.
Examples: Flow reads_from Storage; Transformation reads_from Model.
Not examples: stores, writes_to.
Open questions: Should File be an Entity, Storage, Interface or Integration profile?
```

### 9.3. writes_to

```text
Relation ID: REL-WRITES-TO
Relation name: writes_to
Status: candidate
Source type: Flow, Module, Interface, Transformation
Target type: Storage, Model, Register, File, ExternalSystem
Meaning: Source saves or updates data in target.
Definition: A writes_to relation identifies where data or model updates are persisted.
Required: conditional
Cardinality: many-to-many
Validation rule: Writes should define failure behavior.
Examples: Flow writes_to Storage; Transformation writes_to SDD.
Not examples: returns data without persistence.
Open questions: Should model updates use writes_to or updates?
```

## 10. Boundary relations

### 10.1. accepts

```text
Relation ID: REL-ACCEPTS
Relation name: accepts
Status: candidate
Source type: Interface
Target type: DataField, Event, Command, Entity
Meaning: Source can receive target as input.
Definition: An accepts relation describes input contract of an interface.
Required: conditional
Cardinality: one-to-many
Validation rule: Accepted inputs should have validation rules or documented reason.
Examples: Interface accepts DataField; Interface accepts Event.
Not examples: displays, returns.
Open questions: Should Command be separate element type?
```

### 10.2. returns

```text
Relation ID: REL-RETURNS
Relation name: returns
Status: candidate
Source type: Interface, Flow, Module
Target type: DataField, Entity, Event, Error, Result
Meaning: Source produces target as output.
Definition: A returns relation describes output contract or result.
Required: conditional
Cardinality: one-to-many
Validation rule: Returned errors should be explicit Error elements.
Examples: Interface returns DataField; Interface returns Error.
Not examples: stores, displays.
Open questions: Should outputs from generator use produces instead?
```

### 10.3. exposes

```text
Relation ID: REL-EXPOSES
Relation name: exposes
Status: candidate
Source type: Interface, View
Target type: Entity, DataField, Rule, Error, State
Meaning: Source makes target visible or accessible.
Definition: An exposes relation states what model element can be seen, edited or accessed through a view or interface.
Required: conditional
Cardinality: many-to-many
Validation rule: Exposed data should respect access and validation rules.
Examples: Interface exposes Entity; View exposes Rule.
Not examples: internal implementation use.
Open questions: Distinction between exposes and displays.
```

### 10.4. exchanges_with

```text
Relation ID: REL-EXCHANGES-WITH
Relation name: exchanges_with
Status: candidate
Source type: Integration, Interface, System
Target type: ExternalSystem, Device, Actor, Interface
Meaning: Source exchanges data, events or commands with target.
Definition: An exchanges_with relation identifies an external interaction boundary.
Required: yes for Integration.
Cardinality: many-to-many
Validation rule: Exchange should have interface, data and error behavior.
Examples: Integration exchanges_with PLC; System exchanges_with ERP.
Not examples: internal module dependency.
Open questions: Need ExternalSystem as separate element type?
```

## 11. Architecture relations

### 11.1. provides

```text
Relation ID: REL-PROVIDES
Relation name: provides
Status: candidate
Source type: Module, Layer, System, ExtensionPoint
Target type: Interface, View, Transformation, ValidationRule
Meaning: Source offers target capability or contract.
Definition: A provides relation identifies outward responsibility.
Required: conditional
Cardinality: one-to-many
Validation rule: Provided interface or capability should have contract.
Examples: Module provides Interface; Layer provides View Engine.
Not examples: uses dependency.
Open questions: Should provides be split into provides_interface and provides_capability?
```

### 11.2. uses

```text
Relation ID: REL-USES
Relation name: uses
Status: candidate
Source type: Module, Service, Flow, Transformation, View, TestCase
Target type: Interface, Module, Service, Entity, DataField, Rule, Storage, Model
Meaning: Source relies on target to perform its responsibility.
Definition: A uses relation is a general usage dependency that should be refined when possible.
Required: conditional
Cardinality: many-to-many
Validation rule: Prefer more specific relation when available.
Examples: Module uses Interface; Service uses Entity; Transformation uses Model.
Not examples: contains, implements.
Open questions: When should uses be forbidden as too vague?
```

### 11.2.1. processes

```text
Relation ID: REL-PROCESSES
Relation name: processes
Status: candidate
Source type: Service, Flow, Module
Target type: Entity, DataField, Event, File, Message
Meaning: Source performs meaningful processing over target.
Definition: A processes relation separates active behavior from the information object being processed.
Required: conditional for Service.
Cardinality: many-to-many
Validation rule: If source is Service, it should process, read, write, create, update or expose at least one model element.
Examples: FileScanningService processes SourceFile; StatisticsCalculationService processes TextContent.
Not examples: Entity processes Service.
Open questions: Should processes be split into reads, validates, transforms and aggregates later?
```

### 11.2.2. creates

```text
Relation ID: REL-CREATES
Relation name: creates
Status: candidate
Source type: Service, Flow, Transformation, Task
Target type: Entity, DataField, Event, Report, CodeArtifact, SDDSection
Meaning: Source creates target as a result.
Definition: A creates relation records result production at model level.
Required: conditional
Cardinality: many-to-many
Validation rule: Created target should have owner, lifecycle or storage decision if it persists.
Examples: ReportGenerationService creates Report; FileScanningService creates ScanResult.
Not examples: Module contains Service.
Open questions: Should creates and produces be merged or separated by layer?
```

### 11.3. depends_on

```text
Relation ID: REL-DEPENDS-ON
Relation name: depends_on
Status: candidate
Source type: Module, Layer, View, Transformation, Requirement, CodeArtifact
Target type: Module, Layer, Interface, ModelElement, ExternalSystem, CodeArtifact
Meaning: Source may be affected if target changes.
Definition: A depends_on relation captures architectural, model, implementation or external dependency.
Required: conditional
Cardinality: many-to-many
Validation rule: Dependency must have direction and reason.
Examples: Module depends_on Module; View depends_on ModelElement.
Not examples: visual adjacency, conceptual similarity.
Open questions: Which dependencies are allowed between layers?
```

### 11.4. implements

```text
Relation ID: REL-IMPLEMENTS
Relation name: implements
Status: candidate
Source type: Module, Service, Task, CodeArtifact
Target type: Requirement, Rule, Interface, Flow, Module, Service, TestCase
Meaning: Source realizes target in architecture, work plan or code.
Definition: An implements relation links implementation responsibility to modeled intent.
Required: yes for CodeArtifact when implementation exists.
Cardinality: many-to-many
Validation rule: Implemented target should be verifiable or have OpenQuestion.
Examples: Task implements Requirement; CodeArtifact implements Service; CodeArtifact implements Module.
Not examples: Requirement defines Rule.
Open questions: Direction could be controversial; should CodeArtifact realizes Module be preferred?
```

### 11.4.1. is_implemented_by

```text
Relation ID: REL-IS-IMPLEMENTED-BY
Relation name: is_implemented_by
Status: candidate
Source type: Service, Module, Interface
Target type: CodeArtifact
Meaning: Source has a concrete implementation artifact.
Definition: An is_implemented_by relation connects model-level responsibility or behavior to repository artifacts without merging them into one element.
Required: conditional when implementation exists.
Cardinality: many-to-many
Validation rule: Source should remain a model element; target should have path or code identity.
Examples: FileScanningService is_implemented_by src/scanning/file_scanner.py.
Not examples: CodeArtifact is an Entity.
Open questions: Should this be the primary direction and `implements` only the inverse view?
```

### 11.4.2. defines

```text
Relation ID: REL-DEFINES-CODE
Relation name: defines
Status: candidate
Source type: CodeArtifact
Target type: Class, Function, Schema, ConfigurationItem
Meaning: Code artifact contains or declares a lower-level implementation element.
Definition: A code-level defines relation keeps files, classes and functions in the implementation layer.
Required: optional
Cardinality: many-to-many
Validation rule: Defined target should not be promoted to Entity unless it has model-level data identity.
Examples: src/scanning/file_scanner.py defines class FileScanner.
Not examples: Requirement defines Rule.
Open questions: Should Class and Function become separate element types or remain CodeArtifact subtypes?
```

### 11.5. updates

```text
Relation ID: REL-UPDATES
Relation name: updates
Status: candidate
Source type: Task, Transformation, Flow
Target type: ModelElement, Register, DocumentSection, CodeArtifact, Storage
Meaning: Source changes target.
Definition: An updates relation identifies controlled modification.
Required: conditional
Cardinality: many-to-many
Validation rule: Updates should have source and expected result.
Examples: Task updates CodeArtifact; Transformation updates SDD section.
Not examples: reads_from.
Open questions: Should update be time/version aware?
```

## 12. Verification relations

### 12.1. verifies

```text
Relation ID: REL-VERIFIES
Relation name: verifies
Status: candidate
Source type: TestCase, ValidationRule, Review
Target type: Requirement, Rule, Flow, Interface, Error, StateTransition, CodeArtifact, Model
Meaning: Source checks target against expected result.
Definition: A verifies relation connects a verification method to a model or implementation target.
Required: yes for Requirement through direct or indirect path.
Cardinality: many-to-many
Validation rule: Verification target should have expected result.
Examples: TestCase verifies Rule; TestCase verifies Error handling.
Not examples: Rule validates DataField.
Open questions: Distinction between validates and verifies.
```

### 12.1.1. tests

```text
Relation ID: REL-TESTS
Relation name: tests
Status: candidate
Source type: TestCase
Target type: Service, CodeArtifact, Interface, Flow
Meaning: TestCase exercises a concrete behavior or implementation target.
Definition: A tests relation links a test case to the behavior or artifact it executes, while verifies links it to the expected requirement or rule.
Required: conditional
Cardinality: many-to-many
Validation rule: TestCase tests Service/CodeArtifact may exist only with TestCase verifies Requirement/Rule/Error or reveals_gap RequirementGap.
Examples: TEST-001 tests FileScanningService; TEST-001 verifies REQ-001.
Not examples: TestCase defines Requirement.
Open questions: Should tests remain separate from verifies or be a subtype of verifies?
```

### 12.1.2. reveals_gap

```text
Relation ID: REL-REVEALS-GAP
Relation name: reveals_gap
Status: candidate
Source type: TestCase, ValidationRule, Review
Target type: RequirementGap
Meaning: Source обнаруживает, что для нужной проверки нет ясного Requirement.
Definition: A reveals_gap relation records verification-driven requirement incompleteness without allowing the test to define expected behavior.
Required: yes when TestCase cannot be linked to a clear Requirement.
Cardinality: many-to-many
Validation rule: TestCase with reveals_gap must have status blocked or pending_requirement until Requirement is created or clarified.
Examples: TestCase reveals_gap RequirementGap for undefined empty-folder behavior.
Not examples: failed test against an already clear Requirement.
Open questions: Should RequirementGap be a separate element type or an OpenQuestion subtype?
```

### 12.2. satisfies

```text
Relation ID: REL-SATISFIES
Relation name: satisfies
Status: candidate
Source type: Scenario, Flow, Module, Interface, CodeArtifact
Target type: Requirement, Concern
Meaning: Source contributes to fulfilling target.
Definition: A satisfies relation maps design or behavior to intent.
Required: conditional
Cardinality: many-to-many
Validation rule: Satisfied requirement should still have verification.
Examples: Scenario satisfies Requirement; Module satisfies Concern.
Not examples: Task implements Requirement.
Open questions: Should satisfies be used before implementation only?
```

## 13. Transformation relations

### 13.1. represents

```text
Relation ID: REL-REPRESENTS
Relation name: represents
Status: candidate
Source type: View, Diagram, Table, DocumentSection, Register
Target type: ModelElement, StructuredFact, Model
Meaning: Source is a view of target.
Definition: A represents relation prevents view artifacts from becoming separate sources of truth.
Required: yes for View.
Cardinality: many-to-many
Validation rule: Represented targets should have stable IDs.
Examples: Diagram represents Flow; Register represents Entity elements.
Not examples: contains as source of truth.
Open questions: How to express partial views and filters?
```

### 13.2. conforms_to

```text
Relation ID: REL-CONFORMS-TO
Relation name: conforms_to
Status: candidate
Source type: Model, View, Element, Relation
Target type: Metamodel, Viewpoint, ElementType, RelationType
Meaning: Source follows rules defined by target.
Definition: A conforms_to relation expresses model/metamodel or view/viewpoint compliance.
Required: conditional
Cardinality: many-to-one
Validation rule: Conformance target should be defined.
Examples: Model conforms_to Metamodel; View conforms_to Viewpoint.
Not examples: implements, satisfies.
Open questions: How formal should conformance be before tooling?
```

### 13.3. produces

```text
Relation ID: REL-PRODUCES
Relation name: produces
Status: candidate
Source type: Transformation, Generator, Flow, Task, Module
Target type: View, DocumentSection, SDD, Task, TestCase, CodeArtifact, Report
Meaning: Source creates target as output.
Definition: A produces relation describes generated or created artifacts.
Required: conditional
Cardinality: one-to-many
Validation rule: Produced artifact should state source model or transformation.
Examples: Transformation produces SDD section; Task produces CodeArtifact.
Not examples: stores existing target.
Open questions: Should produced documents be separate element types?
```

### 13.4. generated_from

```text
Relation ID: REL-GENERATED-FROM
Relation name: generated_from
Status: candidate
Source type: View, DocumentSection, TaskList, TestPlan, CodeArtifact
Target type: Model, StructuredFact, Transformation
Meaning: Source was derived from target.
Definition: A generated_from relation provides backward traceability from output to model source.
Required: yes for generated artifacts.
Cardinality: many-to-many
Validation rule: Generated artifact should not be edited as independent truth without recording divergence.
Examples: SDD section generated_from Model; TaskList generated_from Requirement facts.
Not examples: manually authored note without model source.
Open questions: How to handle manually edited generated documents?
```

## 14. Governance relations

### 14.1. sourced_from

```text
Relation ID: REL-SOURCED-FROM
Relation name: sourced_from
Status: candidate
Source type: ModelElement, Relation, StructuredFact, View
Target type: Document, Interview, Standard, Example, UserDecision
Meaning: Source element or fact comes from target evidence.
Definition: A sourced_from relation preserves evidence behind model claims.
Required: yes for important elements and facts.
Cardinality: many-to-many
Validation rule: Important elements without source remain draft or candidate.
Examples: Rule sourced_from Questionnaire answer; Entity sourced_from Example document.
Not examples: arbitrary author memory without reference.
Open questions: How detailed should source references be in Obsidian?
```

### 14.2. affects

```text
Relation ID: REL-AFFECTS
Relation name: affects
Status: candidate
Source type: OpenQuestion, RequirementGap, Decision, Configuration, Requirement, Error
Target type: ModelElement, Relation, View, Transformation, Task, CodeArtifact
Meaning: Source has impact on target.
Definition: An affects relation records influence or uncertainty without pretending to be a final dependency.
Required: conditional
Cardinality: many-to-many
Validation rule: OpenQuestion and RequirementGap should affect at least one model area.
Examples: OpenQuestion affects Rule; RequirementGap affects TestCase; Configuration affects Transformation.
Not examples: verified dependency with clear direction.
Open questions: Should affects be refined into risk/blocks/changes?
```

### 14.2.1. blocked_by

```text
Relation ID: REL-BLOCKED-BY
Relation name: blocked_by
Status: candidate
Source type: TestCase, Task, Transformation, SDDSection
Target type: RequirementGap, OpenQuestion
Meaning: Source cannot be completed correctly until target uncertainty is resolved.
Definition: A blocked_by relation prevents unclear requirements from being silently converted into tests, tasks or generated documents.
Required: conditional
Cardinality: many-to-many
Validation rule: blocked_by target should have owner, status and resolution path.
Examples: TestCase blocked_by RequirementGap; SDDSection blocked_by OpenQuestion.
Not examples: optional improvement that does not block correctness.
Open questions: Should blocked_by be limited to workflow status or remain a model relation?
```

### 14.3. resolves

```text
Relation ID: REL-RESOLVES
Relation name: resolves
Status: candidate
Source type: Task, Decision, Requirement, UserAnswer
Target type: OpenQuestion, RequirementGap, Error, Risk
Meaning: Source closes or answers target.
Definition: A resolves relation links uncertainty or issue to its resolution.
Required: conditional
Cardinality: many-to-many
Validation rule: Resolution should include source and date/status.
Examples: Task resolves OpenQuestion; Requirement resolves RequirementGap; Decision resolves OpenQuestion.
Not examples: ignoring a question.
Open questions: Should Decision become separate element type?
```

## 15. Минимальный набор обязательных связей

На текущем этапе минимальный набор для проверки модели:

| Source | Relation | Target | Почему важно |
|---|---|---|---|
| Project | contains | Requirement | Модель имеет верхний контейнер |
| TestCase | verifies | Requirement | Требование проверяемо |
| TestCase | reveals_gap | RequirementGap | Проверка не подменяет отсутствующее требование |
| TestCase | blocked_by | RequirementGap | Неясное требование блокирует корректную проверку |
| Entity | contains | DataField | Сущность не пустое имя |
| DataField | belongs_to | Entity / Interface / Event | Данные имеют владельца |
| Rule | validates / constrains | DataField / Entity / Flow / Interface | Правило имеет объект применения |
| Rule | raises | Error | Нарушение имеет реакцию |
| Event | triggers | Flow / StateTransition | Причина поведения явна |
| Flow | carries / transfers | DataField / Entity / Event | Понятно, что движется |
| Storage | stores | DataField / Entity / Event / State | Хранение имеет предмет |
| Interface | accepts / returns | DataField / Event / Error | Контракт интерфейса явен |
| Module | provides | Interface | Архитектурная ответственность имеет границу |
| Module | contains | Service | Ответственность отделена от исполнителя поведения |
| Service | uses / processes / creates / updates | Entity | Активное поведение отделено от объекта данных |
| Service | is_implemented_by | CodeArtifact | Модельный исполнитель отделён от файла или класса |
| Task | implements / updates | Requirement / CodeArtifact | Работа трассируется к цели |
| CodeArtifact | implements | Service / Module / Task / TestCase | Код связан с моделью |
| CodeArtifact | defines | Class / Function | Кодовые элементы остаются на implementation layer |
| View | represents | ModelElement / StructuredFact | View не становится source of truth |
| OpenQuestion | affects | ModelElement / Relation / View | Неоднозначность не теряется |
| RequirementGap | affects / resolves | Requirement / TestCase / SDDSection | Разрыв требований виден и закрывается явно |

## 16. Правила качества связей

### 16.1. Связь должна иметь направление

Нельзя фиксировать связь как:

```text
Entity -- DataField
```

Нужно фиксировать:

```text
Entity contains DataField
DataField belongs_to Entity
```

### 16.2. Связь должна иметь тип

Нельзя писать только “связано с”. Нужно выбирать relation type или фиксировать open question о новом типе связи.

### 16.3. Связь должна иметь смысл

Если relation не объясняет, почему элементы связаны, она не помогает модели.

### 16.4. Важная связь должна иметь источник

Связь между важными элементами должна иметь `source`: документ, анкета, пример, решение пользователя, стандарт или проверочный проект.

### 16.5. Диаграммная стрелка не равна relation

Стрелка на диаграмме является view. Relation должна существовать как структурированный факт.

## 17. Открытые вопросы

- Нужно ли вводить отдельный тип `Command`?
- Нужно ли вводить отдельный тип `StateTransition`?
- Нужно ли вводить отдельный тип `Decision`?
- Нужно ли вводить отдельный тип `Concern` и `Stakeholder`, или достаточно Actor/Viewpoint?
- Нужно ли разделять `validates` и `verifies` строго уже сейчас?
- Какие relation types должны быть универсальными, а какие доменными?
- Какие связи должны быть обязательными для первого SDD?
- Как фиксировать cardinality в Markdown/YAML на раннем этапе?

## 18. Связанные документы

### Входные документы

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Передаёт: список кандидатов типов элементов.
  - Используется для: определения source type и target type.
  - Ограничение: не описывает relation types подробно.

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
  - Передаёт: форму Relation Type и Structured Fact.
  - Используется для: структуры этого документа.
  - Ограничение: не задаёт полный список связей.

### Выходные документы

- Будущий [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
  - Получает: relation types.
  - Используется для: формы конкретных утверждений модели.
  - Ограничение: не должен заново определять relation types.

- Будущий [[docs/08_digital_system_cad/metamodel/04_Model_Registers|Model Registers]]
  - Получает: relation types для табличных views.
  - Используется для: отображения связей в реестрах.
  - Ограничение: реестры не должны становиться source of truth.

## 19. История изменений

- Initial version: создан первый список кандидатов relation types для Digital System CAD с направлением, source/target types, meaning, validation rules, examples, not examples и открытыми вопросами.
