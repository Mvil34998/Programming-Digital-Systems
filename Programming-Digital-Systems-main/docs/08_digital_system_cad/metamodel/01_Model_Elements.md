# Model Elements

## 1. Назначение документа

`01_Model_Elements.md` описывает кандидаты типов элементов для рабочей метамодели Digital System CAD.

Документ не является окончательной метамоделью. Он фиксирует текущую инженерную форму, через которую можно собирать информацию о цифровых системах, строить structured facts, формировать реестры, SDD, задачи, тесты и Codex-контекст.

> [!info] Главное
> Элемент модели — это не просто слово и не будущий класс в коде. Важный элемент должен иметь `id`, Definition, Purpose, Context, Source, связи, критерии полноты и открытые вопросы.

## 2. Основание

Документ опирается на:

- [[docs/08_digital_system_cad/00_Digital_System_CAD_Index|Digital System CAD Index]]
- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
- [[docs/08_digital_system_cad/research/01_Metamodeling_Methods_And_Standards|Metamodeling Methods and Standards]]
- [[Digital_System_CAD_Concept_for_Codex|Digital System CAD Concept]]
- [[Digital_System_CAD_Philosophical_Essay_for_Codex|Digital System CAD Philosophical Essay]]
- `docs/05_encyclopedia/`

## 3. Уровни модели

В текущей рабочей форме нужно различать уровни:

| Уровень | Что означает | Пример |
|---|---|---|
| M3 | Правила описания метамоделей | форма Element Type, Relation Type |
| M2 | Метамодель цифровой системы | Entity, DataField, Rule, Flow |
| M1 | Модель конкретной системы | `ENT-001 InputFile`, `RULE-001 RequiredColumnExists` |
| M0 | Реальная система / runtime facts | конкретный файл, ошибка запуска, выполненный тест |

Этот документ работает в основном на уровне M2: он описывает типы элементов, из которых потом будут собираться M1-модели конкретных цифровых систем.

## 4. Универсальная форма Element Type

Каждый тип элемента должен описываться по форме:

```text
Type ID:
Type name:
Status:
Layer:
Definition:
Purpose:
Context:
Not examples:
Required fields:
Optional fields:
Required relations:
Typical relations:
Validation questions:
SDD usage:
Open questions:
```

Минимальные статусы:

- `candidate` — рабочий кандидат, ещё не доказан;
- `accepted` — подтверждён на нескольких проверочных системах;
- `profile-specific` — полезен только в доменном профиле;
- `rejected` — исключён из ядра;
- `deprecated` — заменён другим элементом.

## 5. Сводный список кандидатов

| Type ID              | Type name      | Layer                  | Status    | Purpose                                                        |
| -------------------- | -------------- | ---------------------- | --------- | -------------------------------------------------------------- |
| TYPE-PROJECT         | Project        | Container              | candidate | Верхний контейнер модели цифровой системы                      |
| TYPE-REQUIREMENT     | Requirement    | Intent                 | candidate | Проверяемое требование к системе                               |
| TYPE-REQUIREMENT-GAP | RequirementGap | Intent / Governance    | candidate | Разрыв требований, обнаруженный через нужную проверку           |
| TYPE-ACTOR           | Actor          | Context                | candidate | Участник взаимодействия с системой                             |
| TYPE-SCENARIO        | Scenario       | Behavior               | candidate | Пользовательский или системный сценарий                        |
| TYPE-ENTITY          | Entity         | Domain / System        | candidate | Значимый объект модели                                         |
| TYPE-DATAFIELD       | DataField      | Data                   | candidate | Типизированное поле, значение или параметр                     |
| TYPE-RULE            | Rule           | Constraint             | candidate | Проверяемое условие, ограничение или расчёт                    |
| TYPE-STATE           | State          | Behavior               | candidate | Допустимое положение элемента или системы                      |
| TYPE-EVENT           | Event          | Behavior               | candidate | Факт, запускающий реакцию                                      |
| TYPE-FLOW            | Flow           | Behavior / Interaction | candidate | Направленное движение данных, событий или команд               |
| TYPE-STORAGE         | Storage        | Persistence            | candidate | Требование к сохранению данных, состояний или журналов         |
| TYPE-INTERFACE       | Interface      | Boundary               | candidate | Граница взаимодействия и контракт обмена                       |
| TYPE-INTEGRATION     | Integration    | Boundary               | candidate | Взаимодействие с внешней системой                              |
| TYPE-ERROR           | Error          | Reliability            | candidate | Недопустимая или исключительная ситуация и реакция             |
| TYPE-MODULE          | Module         | Architecture           | candidate | Архитектурная ответственность будущей системы                  |
| TYPE-SERVICE         | Service        | Behavior / Architecture | candidate | Логический исполнитель операции или поведения                  |
| TYPE-LAYER           | Layer          | Architecture           | candidate | Крупная архитектурная область ответственности                  |
| TYPE-MODEL           | Model          | Modeling               | candidate | Структурированное описание конкретной системы                  |
| TYPE-DEPENDENCY      | Dependency     | Architecture           | candidate | Направленная зависимость между элементами                      |
| TYPE-CONFIGURATION   | Configuration  | Variability            | candidate | Изменяемые параметры поведения или views                       |
| TYPE-EXTENSION-POINT | ExtensionPoint | Evolution              | candidate | Управляемая точка расширения                                   |
| TYPE-VIEW            | View           | Representation         | candidate | Представление модели для задачи или аудитории                  |
| TYPE-VIEWPOINT       | Viewpoint      | Representation         | candidate | Правило построения view под concern                            |
| TYPE-TRANSFORMATION  | Transformation | Generation             | candidate | Преобразование модели в SDD, задачи, тесты или context         |
| TYPE-VALIDATION-RULE | ValidationRule | Validation             | candidate | Проверка целостности модели                                    |
| TYPE-TESTCASE        | TestCase       | Verification           | candidate | Проверка требования, правила, сценария или ошибки              |
| TYPE-TASK            | Task           | Implementation         | candidate | Единица работы по изменению модели или реализации              |
| TYPE-CODEARTIFACT    | CodeArtifact   | Implementation         | candidate | Файл, модуль кода, конфигурация или другой артефакт реализации |
| TYPE-OPEN-QUESTION   | OpenQuestion   | Governance             | candidate | Явно зафиксированная неоднозначность                           |

## 6. Core model elements

### 6.0. Правило классификации по роли

Элемент классифицируется не по имени, а по роли в конкретном слое модели.

```text
Если объект является тем, о чём система хранит, обрабатывает, валидирует, передаёт или производит информацию -> Entity.
Если объект группирует архитектурную ответственность -> Module.
Если объект выполняет операцию или поведение -> Service.
Если объект является физическим или логическим артефактом реализации в репозитории -> CodeArtifact.
```

Один концепт может существовать в нескольких слоях как несколько связанных элементов:

```text
Concept: file scanning
Module: ScanningModule
Service: FileScanningService
Entity: SourceFile / ScanJob / ScanResult
CodeArtifact: src/scanning/file_scanner.py
```

Запрещённая форма:

```text
ID: FileScanner
Type: Entity, Module, Service, CodeArtifact
```

Правильная форма:

```text
MOD-001 contains SVC-001
SVC-001 processes ENT-001
SVC-001 creates ENT-002
SVC-001 is_implemented_by CODE-001
```

Правило для Codex: не повышать имя из реализации до Entity только потому, что оно встречается в коде или в названии класса.

### 6.1. Project

```text
Type ID: TYPE-PROJECT
Type name: Project
Status: candidate
Layer: Container
Definition: Project is the top-level container that defines the modeled digital system, its purpose, scope, sources, stakeholders and model boundaries.
Purpose: Hold together all elements, relations, views, transformations and validation rules for one digital system.
Context: Used when creating or validating a complete model of a system.
Not examples: repository folder, company name, one document, implementation task.
Required fields: id, name, definition, purpose, scope, sources, status, open_questions.
Optional fields: stakeholders, constraints, domains, validation_examples.
Required relations: Project contains Requirement; Project has View; Project has OpenQuestion.
Typical relations: Project contains Entity; Project contains Module; Project produces SDD.
Validation questions: Is the system boundary clear? Are sources identified? Are open questions tracked?
SDD usage: top-level spec, scope section, glossary, traceability root.
Open questions: Should Product, System and Project be separate types?
```

### 6.2. Requirement

```text
Type ID: TYPE-REQUIREMENT
Type name: Requirement
Status: candidate
Layer: Intent
Definition: Requirement is a checkable statement about what the system must do, satisfy, prevent, expose, store, verify or support.
Purpose: Convert intent into model facts, tests, tasks and SDD sections.
Context: Used for functional, non-functional, interface, data, reliability and architectural requirements.
Not examples: vague wish, implementation detail, task without required behavior, note without verification.
Required fields: id, name, definition, rationale, source, priority, verification_method, status.
Optional fields: acceptance_criteria, related_stakeholders, constraints, open_questions.
Required relations: TestCase verifies Requirement; Requirement may_be_implemented_by Task. `Requirement is_verified_by TestCase` may be used as a readable inverse view.
Typical relations: Requirement references Entity; Requirement defines Rule; Requirement constrains Interface.
Validation questions: Is it testable? Is source known? Is acceptance criterion clear?
SDD usage: requirements.md, traceability matrix, task generation, test plan.
Open questions: How to classify requirements by viewpoint without duplicating them?
```

### 6.2.1. RequirementGap

```text
Type ID: TYPE-REQUIREMENT-GAP
Type name: RequirementGap
Status: candidate
Layer: Intent / Governance
Definition: RequirementGap фиксирует ситуацию, когда нужна проверка, но в модели нет ясного Requirement, который задаёт ожидаемое поведение системы.
Purpose: Не дать TestCase стать неявным источником поведения. TestCase может обнаружить отсутствующее или неясное требование, но ожидаемое поведение должно быть закреплено в Requirement.
Context: Used when verification need is discovered before the requirement is complete enough to verify.
Not examples: failed test against clear requirement, implementation defect, rejected requirement, ordinary OpenQuestion outside verification.
Required fields: id, name, needed_check, missing_or_unclear_requirement, source, status, resolution_decision.
Optional fields: proposed_requirement, blocked_test_cases, affected_sdd_sections, owner, due_date.
Required relations: TestCase reveals_gap RequirementGap; RequirementGap affects Requirement, Rule, Flow, Error, Module or SDDSection; Requirement resolves RequirementGap after clarification.
Typical statuses: open, pending_requirement, blocked, resolved, rejected.
Validation questions: Какая проверка нужна? Какого Requirement не хватает? Какой TestCase заблокирован? Какой Requirement должен быть создан или обновлён?
SDD usage: open-questions.md, requirements.md, tests.md, traceability matrix.
Open questions: Является ли RequirementGap отдельным element type или строгой специализацией OpenQuestion в будущей метамодели.
```

### 6.3. Actor

```text
Type ID: TYPE-ACTOR
Type name: Actor
Status: candidate
Layer: Context
Definition: Actor is a human, external system, device, role or organization that interacts with the digital system or has a concern.
Purpose: Explain who uses, triggers, receives, configures, verifies or constrains the system.
Context: Used in scenarios, interfaces, requirements, views and architecture descriptions.
Not examples: internal function, data field, anonymous user without role, module.
Required fields: id, name, definition, type, purpose, interaction_context, source.
Optional fields: permissions, concerns, interfaces, open_questions.
Required relations: Actor participates_in Scenario; Actor uses Interface.
Typical relations: Actor has Concern; Actor triggers Event; Actor receives Error.
Validation questions: Is the actor external to the modeled responsibility? Is the role clear?
SDD usage: actors, user roles, external systems, stakeholder concerns.
Open questions: Should Stakeholder and Actor be separate types?
```

### 6.4. Scenario

```text
Type ID: TYPE-SCENARIO
Type name: Scenario
Status: candidate
Layer: Behavior
Definition: Scenario is a structured description of a meaningful path through the system from trigger to result.
Purpose: Capture user/system workflows and connect requirements, events, flows, rules, states and errors.
Context: Used before detailed flows or tests when describing behavior.
Not examples: one event, one state, unordered list of actions, UI description without trigger and result.
Required fields: id, name, definition, trigger, participants, preconditions, main_flow, result.
Optional fields: alternative_flows, error_flows, related_views, open_questions.
Required relations: Scenario is_triggered_by Event; Scenario contains Flow.
Typical relations: Scenario satisfies Requirement; Scenario is_verified_by TestCase.
Validation questions: Is there a trigger? Is there a result? Are errors described?
SDD usage: scenarios.md, use cases, behavior sections, test plan.
Open questions: Should Scenario and Flow be separate in the universal kernel or should Scenario be a view over Flows?
```

## 7. Logical system elements

### 7.1. Entity

```text
Type ID: TYPE-ENTITY
Type name: Entity
Status: candidate
Layer: Domain / System
Definition: Entity is a modeled object that the system identifies, stores, processes, validates, transfers or produces as information.
Purpose: Anchor data, rules, states, events, storage, interfaces and requirements without confusing data objects with executors.
Context: Used for domain objects, system resources, information objects and result objects.
Not examples: random variable, one field, temporary calculation, action, UI label, service name such as FileScanner when it means an executor.
Required fields: id, name, definition, identity_rule, attributes, lifecycle_or_status, context, source.
Optional fields: owner, examples, not_examples, open_questions.
Required relations: Entity contains DataField or has explicit reason why it has no fields.
Typical relations: Entity has State; Entity emits Event; Entity participates_in Flow; Service processes Entity; Storage stores Entity.
Validation questions: Does it have identity? Does it have attributes, lifecycle or status? Is it not Service, Module or CodeArtifact?
SDD usage: entities.md, data model, domain model, glossary.
Open questions: Boundary between Entity, ValueObject, DTO, Record, ViewModel, SystemResource, InformationObject and RuntimeObject.
```

### 7.2. DataField

```text
Type ID: TYPE-DATAFIELD
Type name: DataField
Status: candidate
Layer: Data
Definition: DataField is a typed value, parameter, signal, attribute or message part owned by another model element.
Purpose: Describe what the system receives, stores, validates, transfers or produces.
Context: Used inside entities, interfaces, events, storage, configurations and messages.
Not examples: whole entity, rule, UI control, module, storage technology.
Required fields: id, name, definition, owner, data_type, source, required.
Optional fields: format, units, allowed_values, default_value, validation_rules, open_questions.
Required relations: DataField belongs_to Entity, Interface, Event, Configuration or Storage.
Typical relations: Rule validates DataField; Flow transfers DataField; Storage stores DataField.
Validation questions: Does it have owner? Is format known? Is validation known?
SDD usage: data-model.md, interface contracts, validation rules.
Open questions: Boundary between DataField, Parameter, Signal, Message and Document.
```

### 7.3. Rule

```text
Type ID: TYPE-RULE
Type name: Rule
Status: candidate
Layer: Constraint
Definition: Rule is a checkable condition, constraint, calculation, transition guard, permission or reaction.
Purpose: Make behavior and validity explicit and testable.
Context: Used for data validation, business logic, technical constraints, state transitions and error handling.
Not examples: vague recommendation, library choice, code line, error message without condition.
Required fields: id, name, definition, condition, scope, expected_result, violation_behavior.
Optional fields: severity, examples, related_states, related_events, open_questions.
Required relations: Rule constrains at least one Entity, DataField, State, Flow, Interface or Requirement.
Typical relations: Rule validates DataField; Rule raises Error; TestCase verifies Rule.
Validation questions: Is the condition checkable? Is violation behavior known?
SDD usage: rules.md, requirements, test plan, error behavior.
Open questions: How to express rules declaratively in early Markdown/YAML form?
```

### 7.4. State

```text
Type ID: TYPE-STATE
Type name: State
Status: candidate
Layer: Behavior
Definition: State is a defined condition of a system, entity, process, interface, data item or equipment that affects allowed behavior.
Purpose: Describe allowed actions, forbidden actions and transitions.
Context: Used where behavior depends on mode, phase, status or lifecycle.
Not examples: event, action, random flag, process step without entry/exit conditions.
Required fields: id, name, definition, owner, entry_condition, allowed_actions, exit_condition.
Optional fields: forbidden_actions, related_errors, UI_representation, open_questions.
Required relations: State belongs_to Entity, Flow, Interface, System or DataField.
Typical relations: Event triggers State transition; Rule guards State transition.
Validation questions: Does it affect behavior? Are transitions known?
SDD usage: states.md, state diagrams, behavioral requirements.
Open questions: Boundary between State, Mode, Phase, Status and ErrorState.
```

### 7.5. Event

```text
Type ID: TYPE-EVENT
Type name: Event
Status: candidate
Layer: Behavior
Definition: Event is a fact, signal, message, action or condition occurrence that requires or records a system reaction.
Purpose: Connect causes with flows, state transitions, rules and errors.
Context: Used for user actions, system events, data changes, timers, hardware signals and error events.
Not examples: long process, state, rule, UI element, message without source and reaction.
Required fields: id, name, definition, source, cause, allowed_states, reaction.
Optional fields: event_data, timestamp_rule, result, possible_errors, open_questions.
Required relations: Event triggers Flow or State transition.
Typical relations: Event carries DataField; Event may_raise Error; Rule handles Event.
Validation questions: Is source known? Is reaction known? Is allowed state known?
SDD usage: events.md, sequence diagrams, state diagrams, test scenarios.
Open questions: Boundary between Event, Command, Signal, Message and Notification.
```

### 7.6. Flow

```text
Type ID: TYPE-FLOW
Type name: Flow
Status: candidate
Layer: Behavior / Interaction
Definition: Flow is directed movement of data, commands, events, states, errors or results from source to target.
Purpose: Describe how things move through the system and where rules/errors apply.
Context: Used for data flows, user flows, integration flows, storage flows and error flows.
Not examples: diagram arrow without transmitted object, unordered steps, dependency without route.
Required fields: id, name, definition, source, target, transferred_object, trigger, result.
Optional fields: preconditions, steps, postconditions, possible_errors, open_questions.
Required relations: Flow has source and target; Flow transfers or moves a model element.
Typical relations: Event triggers Flow; Rule guards Flow; Flow writes_to Storage.
Validation questions: Is source known? Is target known? Is transmitted object known?
SDD usage: flows.md, scenarios, diagrams, integration descriptions.
Open questions: Boundary between Flow, Process, Scenario, Dependency and Interaction.
```

### 7.7. Storage

```text
Type ID: TYPE-STORAGE
Type name: Storage
Status: candidate
Layer: Persistence
Definition: Storage is a model element describing what must be persisted, why, by whom, for how long and under which integrity rules.
Purpose: Separate persistence requirements from technology choice.
Context: Used for files, databases, logs, archives, configuration stores and model repositories.
Not examples: SQLite as a decision without requirements, temporary variable, file name without structure.
Required fields: id, name, definition, stored_elements, purpose, owner, lifecycle.
Optional fields: retention, integrity_rules, access_rules, recovery_rules, open_questions.
Required relations: Storage stores DataField, Entity, Event, State, Configuration or Result.
Typical relations: Flow reads_from Storage; Flow writes_to Storage; Error occurs_in Storage.
Validation questions: Why is it persisted? Who reads it? What integrity rules exist?
SDD usage: storage.md, persistence requirements, backup/recovery sections.
Open questions: Boundary between Storage, Repository, Archive, Log, Cache and ConfigurationStore.
```

### 7.8. Interface

```text
Type ID: TYPE-INTERFACE
Type name: Interface
Status: candidate
Layer: Boundary
Definition: Interface is a boundary of interaction with defined participants, input, output, commands, events, errors and contract.
Purpose: Make interaction explicit and independent from internal implementation.
Context: Used for UI, API, CLI, files, hardware signals, module contracts and test interfaces.
Not examples: button without action/data, endpoint without contract, module without boundary.
Required fields: id, name, definition, participants, purpose, input_data, output_data, errors.
Optional fields: commands, events, states, protocol, format, version, open_questions.
Required relations: Interface accepts or returns DataField, Event, Error or Command.
Typical relations: Module provides Interface; Actor uses Interface; Flow calls Interface.
Validation questions: Are participants known? Is contract known? Are errors defined?
SDD usage: interfaces.md, API contracts, UI requirements, integration contracts.
Open questions: Boundary between Interface, Port, API, UI, Protocol, FileFormat and Connector.
```

### 7.9. Integration

```text
Type ID: TYPE-INTEGRATION
Type name: Integration
Status: candidate
Layer: Boundary
Definition: Integration is a modeled relationship and exchange contract between the system and an external system, device, service, file source or environment.
Purpose: Describe external dependencies and exchange behavior.
Context: Used for APIs, PLC/HMI exchange, file import/export, ERP/CAM/CNC links, external services.
Not examples: internal module call, generic dependency, library import, vague external mention.
Required fields: id, name, definition, external_party, purpose, exchanged_data, interface, errors.
Optional fields: protocol, frequency, authentication, availability, open_questions.
Required relations: Integration uses Interface; Integration exchanges DataField or Event.
Typical relations: Integration may_raise Error; Flow interacts_with Integration.
Validation questions: Is external boundary clear? Is exchanged data defined?
SDD usage: integrations.md, external systems, interface contracts.
Open questions: Should Integration be separate from Interface or be a profile of Interface?
```

### 7.10. Error

```text
Type ID: TYPE-ERROR
Type name: Error
Status: candidate
Layer: Reliability
Definition: Error is an invalid, exceptional, unsafe or unresolved condition and the required system reaction.
Purpose: Make negative scenarios explicit and testable.
Context: Used for invalid data, rule violation, unavailable resources, integration failure, unsafe state and user-visible problems.
Not examples: traceback without model meaning, vague failure, message without cause, open question.
Required fields: id, name, definition, source, cause, trigger_condition, severity, reaction.
Optional fields: user_message, recovery, logging_rule, related_state, open_questions.
Required relations: Error caused_by Rule violation, DataField, State, Flow, Storage, Interface or Integration.
Typical relations: Rule raises Error; Flow handles Error; TestCase verifies Error handling.
Validation questions: Is cause known? Is severity known? Is reaction known?
SDD usage: errors.md, negative scenarios, reliability requirements, test plan.
Open questions: Boundary between Error, Warning, Fault, Alarm, Exception and OpenQuestion.
```

## 8. Architecture and implementation elements

### 8.1. Module

```text
Type ID: TYPE-MODULE
Type name: Module
Status: candidate
Layer: Architecture
Definition: Module is an architectural responsibility boundary that groups related services, rules, entities, interfaces or code artifacts.
Purpose: Bridge logical model and implementation architecture without becoming an executor or premature file/class decision.
Context: Used after logical elements and flows are clear enough to group responsibilities.
Not examples: any code file, random function group, technology library, domain entity, single operation when Service is more precise.
Required fields: id, name, definition, responsibility, layer, input, output, verification_criteria.
Optional fields: services, provided_interfaces, used_interfaces, handled_errors, code_artifacts, open_questions.
Required relations: Module belongs_to Layer or Architecture; Module contains Service or provides Interface.
Typical relations: Module contains Service; Module provides Interface; Service is_implemented_by CodeArtifact.
Validation questions: Is responsibility narrow? Are contained services explicit? Are dependencies explicit?
SDD usage: architecture.md, modules.md, implementation plan.
Open questions: Boundary between Module, Component, Service, Adapter, Layer and CodeArtifact.
```

### 8.2. Service

```text
Type ID: TYPE-SERVICE
Type name: Service
Status: candidate
Layer: Behavior / Architecture
Definition: Service is a logical executor of an operation or behavior that acts on entities but is not itself the primary stored domain object.
Purpose: Separate active behavior from Entity, Module and CodeArtifact.
Context: Used for application services, domain services, infrastructure services, calculators, readers, writers, scanners and validators.
Not examples: domain object with identity, architecture area, physical source file, class name without modeled operation.
Required fields: id, name, operation, responsibility, input, output, owner_module, status.
Optional fields: preconditions, postconditions, errors, code_artifacts, open_questions.
Required relations: Module contains Service; Service processes/creates/updates Entity or uses Storage; Service is_implemented_by CodeArtifact when implementation is known.
Typical relations: Service exposes Interface; TestCase tests Service; Service handles Error; Service satisfies Flow.
Validation questions: What operation does it perform? What Entity does it use or produce? Which Module owns it? Which CodeArtifact implements it?
SDD usage: architecture.md, flows.md, implementation.md, tests.md.
Open questions: Boundary between Service, Module, Adapter, UseCase and Function.
```

### 8.3. Layer

```text
Type ID: TYPE-LAYER
Type name: Layer
Status: candidate
Layer: Architecture
Definition: Layer is a major architectural responsibility area grouping modules, models, interfaces and dependency rules.
Purpose: Control dependency direction and separation of concerns.
Context: Used for model repository, metamodel registry, view engine, validation engine, transformation engine and import/export layer.
Not examples: folder, one module, framework, diagram block without dependency rules.
Required fields: id, name, definition, responsibility, allowed_dependencies, forbidden_dependencies.
Optional fields: contained_modules, provided_interfaces, validation_rules, open_questions.
Required relations: Layer contains Module or has explicit reason why it is abstract.
Typical relations: Layer depends_on Layer; Rule constrains Layer.
Validation questions: Are dependency rules clear? Is responsibility distinct?
SDD usage: architecture.md, dependency rules, implementation architecture.
Open questions: Which layers are mandatory for Digital System CAD itself?
```

### 8.3. Model

```text
Type ID: TYPE-MODEL
Type name: Model
Status: candidate
Layer: Modeling
Definition: Model is a structured description of a concrete system or part of a system built according to a metamodel.
Purpose: Act as source of truth for views, transformations, validation and traceability.
Context: Used for M1 models of concrete systems.
Not examples: free text, diagram without elements, code class without metamodel relation, SDD as sole source of truth.
Required fields: id, name, definition, metamodel, elements, relations, sources.
Optional fields: views, validation_rules, transformations, open_questions.
Required relations: Model conforms_to Metamodel; Model contains ModelElement.
Typical relations: View represents Model; Transformation reads Model.
Validation questions: Are elements typed? Are relations typed? Are sources known?
SDD usage: source for SDD sections and traceability.
Open questions: Minimal storage format for early model repository.
```

### 8.4. Dependency

```text
Type ID: TYPE-DEPENDENCY
Type name: Dependency
Status: candidate
Layer: Architecture
Definition: Dependency is a typed directed relation showing that one element uses, requires, calls, reads, writes, implements or constrains another element.
Purpose: Make coupling explicit and checkable.
Context: Used for architecture, modules, layers, interfaces, requirements and transformations.
Not examples: visual proximity, thematic similarity, relation without direction or reason.
Required fields: id, source, target, kind, reason, direction, required.
Optional fields: stability, risk, isolation_strategy, open_questions.
Required relations: Dependency connects two typed elements.
Typical relations: Module depends_on Module; Layer depends_on Layer; View depends_on ModelElement.
Validation questions: Is direction clear? Is reason clear? Is risk known?
SDD usage: dependency diagrams, architecture constraints, risk analysis.
Open questions: Controlled vocabulary of dependency kinds.
```

### 8.5. Configuration

```text
Type ID: TYPE-CONFIGURATION
Type name: Configuration
Status: candidate
Layer: Variability
Definition: Configuration is a typed element defining changeable parameters of behavior, environment, generation, validation, views or import/export without changing model logic.
Purpose: Separate adjustable parameters from rules and implementation code.
Context: Used for settings, thresholds, generators, view options, import/export mappings and Codex-context options.
Not examples: hidden business rule, magic value, technology choice without purpose.
Required fields: id, name, definition, scope, parameters, allowed_values, validation_rules.
Optional fields: defaults, owner, storage, open_questions.
Required relations: Configuration sets Parameter or affects Rule, View, Transformation or Interface.
Typical relations: Rule validates Configuration; Storage stores Configuration.
Validation questions: Is scope known? Are allowed values known? Is it not a hidden rule?
SDD usage: configuration.md, operational settings, generation settings.
Open questions: Which Digital System CAD behaviors must be configurable?
```

### 8.6. ExtensionPoint

```text
Type ID: TYPE-EXTENSION-POINT
Type name: ExtensionPoint
Status: candidate
Layer: Evolution
Definition: ExtensionPoint is a controlled place where new metamodels, element types, relation types, views, validators, transformations, generators or adapters can be added.
Purpose: Preserve future extensibility without uncontrolled architecture growth.
Context: Used mostly for future Digital System CAD architecture, not for immediate implementation.
Not examples: arbitrary code insertion, workaround, configuration value without new behavior.
Required fields: id, name, definition, purpose, extension_contract, allowed_extensions, forbidden_extensions.
Optional fields: affected_layers, dependencies, validation_rules, open_questions.
Required relations: ExtensionPoint requires Interface or Transformation contract.
Typical relations: ExtensionPoint affects View; ExtensionPoint accepts Extension.
Validation questions: Is contract clear? Are limits clear? Is extension necessary?
SDD usage: architecture evolution, plugin/extension requirements.
Open questions: Required extension points for future Digital System CAD.
```

## 9. Representation and transformation elements

### 9.1. View

```text
Type ID: TYPE-VIEW
Type name: View
Status: candidate
Layer: Representation
Definition: View is a representation of selected model elements and relations for a purpose, audience and viewpoint.
Purpose: Prevent diagrams, tables, forms and documents from becoming separate sources of truth.
Context: Used for diagrams, registers, forms, SDD sections, task lists, test plans and Codex context.
Not examples: separate manually maintained truth, screenshot, document without source model.
Required fields: id, name, definition, purpose, audience, viewpoint, source_elements, source_relations.
Optional fields: shown_fields, hidden_fields, grouping_rules, sorting_rules, output_format, open_questions.
Required relations: View represents ModelElement or StructuredFact.
Typical relations: View conforms_to Viewpoint; Transformation produces View.
Validation questions: Is source model known? Is audience known? Are shown fields defined?
SDD usage: all SDD sections are views or transformation outputs.
Open questions: How to express correspondence rules between views?
```

### 9.2. Viewpoint

```text
Type ID: TYPE-VIEWPOINT
Type name: Viewpoint
Status: candidate
Layer: Representation
Definition: Viewpoint is a rule for constructing views that address specific stakeholder concerns.
Purpose: Avoid one universal representation and support multiple views of one model.
Context: Inspired by ISO 42010 and used for requirements, architecture, data, testing, implementation and Codex-context views.
Not examples: diagram style, audience label without concern, arbitrary filter.
Required fields: id, name, definition, stakeholder, concern, allowed_views, relevant_element_types.
Optional fields: relevant_relation_types, correspondence_rules, open_questions.
Required relations: Viewpoint frames View.
Typical relations: Stakeholder has Concern; View conforms_to Viewpoint.
Validation questions: Is concern clear? Are allowed views clear?
SDD usage: defines structure of SDD sections and diagrams.
Open questions: Minimal viewpoint set for Digital System CAD.
```

### 9.3. Transformation

```text
Type ID: TYPE-TRANSFORMATION
Type name: Transformation
Status: candidate
Layer: Generation
Definition: Transformation is a rule-based conversion from model elements and relations into another model, view, document, task list, test plan or Codex context.
Purpose: Treat generation as structured model transformation, not free text rendering.
Context: Used for model -> SDD, model -> diagram, questionnaire -> model, model -> tasks, model -> tests.
Not examples: manual copy-paste, prompt without structured input, uncontrolled text generation.
Required fields: id, name, definition, input_elements, input_relations, output, rules.
Optional fields: validation_before, validation_after, output_format, open_questions.
Required relations: Transformation reads Model or View; Transformation produces View or Artifact.
Typical relations: Transformation produces SDD section; Transformation produces Task.
Validation questions: Are inputs typed? Are rules explicit? Is output checkable?
SDD usage: SDD generation rules, Codex context generation.
Open questions: How formal should transformations be in the Markdown prototype?
```

### 9.4. ValidationRule

```text
Type ID: TYPE-VALIDATION-RULE
Type name: ValidationRule
Status: candidate
Layer: Validation
Definition: ValidationRule is a check that evaluates completeness, consistency, traceability or correctness of model elements and relations.
Purpose: Make model quality explicit and eventually machine-checkable.
Context: Used for required fields, required relations, ID policies, traceability and view consistency.
Not examples: style preference, vague review note, implementation test without model target.
Required fields: id, name, definition, applies_to, condition, expected_result, severity.
Optional fields: violation_message, related_sdd_section, related_testcase, open_questions.
Required relations: ValidationRule checks ElementType, RelationType, StructuredFact, View or Transformation.
Typical relations: ValidationRule raises OpenQuestion; ValidationRule blocks Transformation.
Validation questions: Is condition checkable? Is severity known?
SDD usage: model quality gates before SDD generation.
Open questions: Which validation rules are blockers for first SDD?
```

## 10. Verification and implementation trace elements

### 10.1. TestCase

```text
Type ID: TYPE-TESTCASE
Type name: TestCase
Status: candidate
Layer: Verification
Definition: TestCase is a defined check of requirement, rule, scenario, flow, interface, state transition, error handling or code artifact.
Purpose: Close the loop between model, SDD and verification.
Context: Used for positive and negative scenarios, acceptance tests, unit tests, integration tests and manual checks.
Not examples: vague check, test file without purpose, QA note without expected result.
Required fields: id, name, definition, target, preconditions, steps, expected_result, verification_type.
Optional fields: test_data, automation_status, related_code, open_questions.
Required relations: TestCase verifies Requirement, Rule, Flow, Interface, Error, Task or CodeArtifact.
Typical relations: Requirement is_verified_by TestCase; Error handling is_verified_by TestCase.
Validation questions: Is target known? Is expected result known?
SDD usage: tests.md, acceptance criteria, traceability.
Open questions: How to distinguish TestCase, ValidationRule and AcceptanceCriterion?
```

### 10.2. Task

```text
Type ID: TYPE-TASK
Type name: Task
Status: candidate
Layer: Implementation
Definition: Task is a unit of work that changes model, documentation, code, tests, configuration or validation artifacts.
Purpose: Connect requirements and model decisions to implementation work.
Context: Used for Codex tasks, developer tasks, documentation tasks and validation tasks.
Not examples: requirement, note, open question, untraceable to-do.
Required fields: id, name, definition, purpose, source, expected_output, status.
Optional fields: owner, priority, affected_elements, affected_artifacts, open_questions.
Required relations: Task implements Requirement, resolves OpenQuestion, updates ModelElement or changes CodeArtifact.
Typical relations: Task produces CodeArtifact; Task is_verified_by TestCase.
Validation questions: Is source known? Is expected output known? Is traceability known?
SDD usage: tasks.md, implementation plan, Codex task context.
Open questions: How granular should tasks be for Codex?
```

### 10.3. CodeArtifact

```text
Type ID: TYPE-CODEARTIFACT
Type name: CodeArtifact
Status: candidate
Layer: Implementation
Definition: CodeArtifact is a file, module, package, schema, configuration, test file or generated artifact that realizes part of the model or task.
Purpose: Provide reverse traceability from implementation to model.
Context: Used after implementation begins or when analyzing existing systems.
Not examples: abstract module without file, requirement, diagram, unrelated generated output.
Required fields: id, name, definition, artifact_type, path_or_location, responsibility, status.
Optional fields: generated_from, related_tests, owner, open_questions.
Required relations: CodeArtifact implements Service, Module, Task, Rule, Interface, TestCase or Transformation output.
Typical relations: Service is_implemented_by CodeArtifact; Task changes CodeArtifact; TestCase verifies CodeArtifact; CodeArtifact defines Class or Function.
Validation questions: Is artifact linked to model intent? Is path known? Is verification known?
SDD usage: implementation architecture, traceability, code context for Codex.
Open questions: How to represent generated artifacts versus hand-written artifacts?
```

### 10.4. OpenQuestion

```text
Type ID: TYPE-OPEN-QUESTION
Type name: OpenQuestion
Status: candidate
Layer: Governance
Definition: OpenQuestion is an explicit unresolved uncertainty that should not be guessed or silently converted into a model fact.
Purpose: Preserve rigor when the model lacks evidence, definition or boundary. RequirementGap is a stricter OpenQuestion case for missing or unclear requirements discovered through verification needs.
Context: Used whenever element type, relation, field, source, validation or interpretation is unclear.
Not examples: known error, rejected requirement, vague note without owner/context.
Required fields: id, question, context, source, affected_elements, status.
Optional fields: options, decision_needed_by, resolution, related_tasks.
Required relations: OpenQuestion affects ModelElement, RelationType, StructuredFact, View or Transformation.
Typical relations: Task resolves OpenQuestion; Decision resolves OpenQuestion.
Validation questions: Is uncertainty explicit? Is affected model area known?
SDD usage: open-questions.md, risks, unresolved assumptions.
Open questions: Should Decision be a separate type from OpenQuestion resolution?
```

## 11. Минимальные поля конкретного элемента

Каждый конкретный элемент M1 должен иметь минимум:

```yaml
id:
type:
name:
definition:
purpose:
source:
status:
context:
open_questions:
```

Если у элемента нет Definition, Purpose, Source или Context, он не должен считаться достаточно определённым.

## 12. Первичные правила полноты

### 12.1. Обязательные поля

- Каждый element type должен иметь Definition.
- Каждый element instance должен иметь stable ID.
- Каждый важный элемент должен иметь Source.
- Каждый важный элемент должен иметь Open questions, даже если список пуст.

### 12.2. Обязательные связи

- Requirement должен иметь TestCase или OpenQuestion/RequirementGap о способе проверки.
- TestCase не должен задавать ожидаемое поведение вместо Requirement. Если проверка нужна, но Requirement неясен или отсутствует, нужно создать RequirementGap.
- DataField должен иметь owner.
- Rule должен иметь target и violation behavior.
- Error должен иметь cause и reaction.
- Interface должен иметь input/output или объяснение, почему одно из них отсутствует.
- Flow должен иметь source, target и transferred object.
- Task должен иметь traceability source.
- CodeArtifact должен иметь связь с Task, Service, Module, TestCase или Transformation.

### 12.3. Запреты

- Не считать имя определением.
- Не считать диаграмму моделью.
- Не считать таблицу source of truth.
- Не добавлять архитектурный модуль до появления логической причины.
- Не превращать open question в факт без источника.

## 13. Связанные документы

### Входные документы

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
  - Передаёт: форму Element Type и Element Card.
  - Используется для: структуры этого документа.
  - Ограничение: не перечисляет конкретные кандидаты подробно.

- [[docs/08_digital_system_cad/00_Digital_System_CAD_Index|Digital System CAD Index]]
  - Передаёт: место документа в слое Digital System CAD.
  - Используется для: согласования порядка работ.
  - Ограничение: не заменяет этот документ.

- [[docs/05_encyclopedia/Entities|Entities]]
  - Передаёт: пример метамодельной интерпретации базового понятия.
  - Используется для: формирования кандидата Entity.
  - Ограничение: не является M2-спецификацией всех элементов.

### Выходные документы

- Будущий [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Получает: список типов элементов.
  - Используется для: описания допустимых typed relations.
  - Ограничение: не должен заново определять элементы.

- Будущий [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
  - Получает: элементы как subject/object structured facts.
  - Используется для: формата проверяемых утверждений модели.
  - Ограничение: не должен подменять список типов элементов.

## 14. История изменений

- Initial version: создан первый список кандидатов типов элементов модели Digital System CAD с определениями, назначением, обязательными полями, связями, проверками полноты и открытыми вопросами.
