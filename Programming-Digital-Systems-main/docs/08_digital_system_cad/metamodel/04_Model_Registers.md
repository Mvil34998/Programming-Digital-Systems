# Model Registers

## 1. Назначение документа

`04_Model_Registers.md` описывает реестры модели Digital System CAD.

Register — это табличное view над model elements и structured facts. Реестр помогает видеть модель, проверять полноту, сортировать элементы и готовить SDD, но не должен становиться отдельным источником правды.

> [!info] Главное
> Реестр — это view модели. Если в таблице появляется новый смысл, он должен быть возвращён в модель как element, relation или structured fact.

## 2. Основание

Документ опирается на:

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
- [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]

## 3. Что такое register

Register — это табличное представление элементов одного типа или группы связанных фактов.

Минимальный register показывает:

- какие элементы существуют;
- какие ID заняты;
- какие элементы неполные;
- какие связи обязательны;
- какие open questions есть;
- какие элементы попадают в SDD, views, tests или Codex context.

Register не решает:

- окончательную полноту метамодели;
- доказательство универсальности элементов;
- выбор инструмента хранения;
- генерацию SDD без validation rules.

## 4. Общие правила registers

### 4.1. Register is a view

Реестр не является source of truth.

Source of truth:

```text
typed elements + typed relations + structured facts
```

Register:

```text
табличный view над source of truth
```

### 4.2. Every row must have stable ID

Каждая строка реестра должна ссылаться на stable ID элемента или факта.

### 4.3. No anonymous rows

Если строка не имеет ID, она является заметкой, а не частью модели.

### 4.4. Open questions must be visible

Реестр должен показывать, где элемент неполон или неоднозначен.

### 4.5. Required relations must be visible

Если для элемента есть обязательные связи, реестр должен показывать их наличие или отсутствие.

## 5. Универсальная форма register

Минимальная форма:

```text
ID | Type | Name | Status | Definition | Source | Required relations | Validation status | Open questions
```

Расширенная форма:

```text
ID | Type | Name | Status | Definition | Purpose | Context | Source | Related facts | Used in views | Used in SDD | Validation status | Open questions
```

## 6. ID prefixes

Предварительные prefixes:

| Prefix | Element type |
|---|---|
| `PRJ` | Project |
| `REQ` | Requirement |
| `ACT` | Actor |
| `SCN` | Scenario |
| `ENT` | Entity |
| `DATA` | DataField |
| `RULE` | Rule |
| `STATE` | State |
| `EVENT` | Event |
| `FLOW` | Flow |
| `STOR` | Storage |
| `INT` | Interface |
| `INTEG` | Integration |
| `ERR` | Error |
| `MOD` | Module |
| `SVC` | Service |
| `LAYER` | Layer |
| `MODEL` | Model |
| `DEP` | Dependency |
| `CONF` | Configuration |
| `EXT` | ExtensionPoint |
| `VIEW` | View |
| `VP` | Viewpoint |
| `TR` | Transformation |
| `VAL` | ValidationRule |
| `TEST` | TestCase |
| `RGAP` | RequirementGap |
| `TASK` | Task |
| `CODE` | CodeArtifact |
| `OQ` | OpenQuestion |
| `FACT` | StructuredFact |

Open question:

- Нужно ли использовать короткие prefixes (`DF`) или смысловые prefixes (`DATA`)?
- Нужно ли фиксировать profile prefix для доменных расширений?

## 7. Core registers

### 7.1. Projects Register

Назначение: показывать верхние контейнеры моделей.

```text
ID | Name | Definition | Scope | Sources | Status | Open questions
```

Required checks:

- Project has definition;
- Project has scope;
- Project has at least one source;
- Project has open questions list.

### 7.2. Requirements Register

Назначение: показывать проверяемые требования.

```text
ID | Name | Definition | Type | Priority | Source | Verified by | Status | Open questions
```

Required facts:

- `Project contains Requirement`;
- `Requirement is_verified_by TestCase` or OpenQuestion/RequirementGap;
- `Requirement references ModelElement` when applicable.

Used in SDD:

- `requirements.md`;
- traceability matrix;
- task generation.

### 7.3. Actors Register

Назначение: показывать участников взаимодействия и заинтересованные роли.

```text
ID | Name | Type | Definition | Purpose | Interfaces | Scenarios | Concerns | Open questions
```

Required facts:

- `Actor participates_in Scenario` or OpenQuestion;
- `Actor uses Interface` when interaction exists.

### 7.4. Scenarios Register

Назначение: показывать сценарии от trigger до result.

```text
ID | Name | Trigger | Participants | Main flow | Result | Error flows | Verified by | Open questions
```

Required facts:

- `Scenario is_triggered_by Event`;
- `Scenario contains Flow`;
- `Scenario satisfies Requirement` when scenario supports requirement.

## 8. Logical model registers

### 8.1. Entities Register

```text
ID | Name | Type | Definition | Purpose | Data fields | States | Events | Storage | Open questions
```

Required facts:

- `Entity contains DataField` or documented reason;
- `Entity has State` if lifecycle matters;
- `Storage stores Entity` if persistence is required.

Used in SDD:

- `entities.md`;
- `data-model.md`;
- glossary.

### 8.2. DataFields Register

```text
ID | Name | Owner | Data type | Required | Format | Allowed values | Validated by | Error behavior | Open questions
```

Required facts:

- `DataField belongs_to Entity / Interface / Event / Configuration`;
- `Rule validates DataField` for critical fields;
- `Error caused_by DataField` when invalid data has negative scenario.

### 8.3. Rules Register

```text
ID | Name | Kind | Condition | Target | Expected result | Violation behavior | Raises error | Verified by | Open questions
```

Required facts:

- `Rule validates / constrains target`;
- `Rule raises Error` for critical violations;
- `TestCase verifies Rule` or OpenQuestion.

### 8.4. States Register

```text
ID | Name | Owner | Definition | Entry condition | Allowed actions | Exit condition | Events | Errors | Open questions
```

Required facts:

- `State belongs_to owner`;
- `Event triggers StateTransition` when behavior is modeled;
- `Rule guards StateTransition` when transition has condition.

### 8.5. Events Register

```text
ID | Name | Source | Cause | Event data | Allowed states | Triggers | Reaction | Errors | Open questions
```

Required facts:

- `Event triggers Flow / StateTransition`;
- `Event carries DataField` if event has data;
- `Event may_raise Error` if handling can fail.

### 8.6. Flows Register

```text
ID | Name | Kind | Source | Target | Transferred object | Trigger | Rules | Errors | Result | Open questions
```

Required facts:

- `Flow has source`;
- `Flow has target`;
- `Flow transfers / carries DataField, Entity or Event`;
- `Flow may_raise Error` for critical flows.

### 8.7. Storage Register

```text
ID | Name | Kind | Stored elements | Purpose | Owner | Lifecycle | Integrity rules | Errors | Open questions
```

Required facts:

- `Storage stores DataField / Entity / Event / State / Configuration`;
- `Flow reads_from Storage` or `Flow writes_to Storage`;
- `Error occurs_in Storage` for storage failures.

### 8.8. Interfaces Register

```text
ID | Name | Kind | Participants | Input | Output | Commands / Events | Errors | Provider | Open questions
```

Required facts:

- `Interface accepts DataField / Event / Command`;
- `Interface returns DataField / Error`;
- `Module provides Interface` when architecture exists.

### 8.9. Integrations Register

```text
ID | Name | External system | Interface | Exchanged data | Protocol / format | Errors | Owner | Open questions
```

Required facts:

- `Integration uses Interface`;
- `Integration exchanges_with ExternalSystem`;
- `Integration exchanges DataField / Event`;
- `Integration may_raise Error`.

### 8.10. Errors Register

```text
ID | Name | Kind | Source | Cause | Severity | Reaction | Recovery | Logging | Verified by | Open questions
```

Required facts:

- `Error caused_by Rule / DataField / State / Flow / Storage / Interface`;
- `Flow handles Error` or `Interface returns Error`;
- `TestCase verifies Error handling` for critical errors.

## 9. Architecture registers

### 9.1. Layers Register

```text
ID | Name | Responsibility | Allowed dependencies | Forbidden dependencies | Modules | Interfaces | Open questions
```

Required facts:

- `Layer contains Module`;
- `Layer depends_on Layer` if dependency exists;
- `Rule constrains Layer` for dependency rules.

### 9.2. Modules Register

```text
ID | Name | Layer | Responsibility | Services | Input | Output | Provides | Uses | Handles errors | Verified by | Open questions
```

Required facts:

- `Module belongs_to Layer`;
- `Module contains Service` when behavior is decomposed;
- `Module provides Interface`;
- `Module uses Interface / Module / Storage` when applicable.

### 9.2.1. Services Register

Назначение: отделить исполнителей поведения от Module, Entity и CodeArtifact.

```text
ID | Name | Owner Module | Operation | Input | Output | Processes | Creates / Updates | Interfaces | Implemented by | Tested by | Open questions
```

Required facts:

- `Module contains Service`;
- `Service processes / creates / updates Entity` or documented reason;
- `Service is_implemented_by CodeArtifact` when implementation is known;
- `TestCase tests Service` when behavior is verified directly.

Rule:

- Имена вида `FileScanner`, `FileReader`, `StatsCalculator`, `ReportWriter`, `Logger` не становятся Entity по умолчанию. Сначала нужно проверить, не являются ли они Service, Module или CodeArtifact.

### 9.3. Dependencies Register

```text
ID | Source | Relation | Target | Kind | Reason | Required | Risk | Isolation strategy | Open questions
```

Required facts:

- `Dependency connects source and target`;
- dependency direction is explicit;
- dependency reason is explicit.

### 9.4. Configurations Register

```text
ID | Name | Scope | Parameters | Defaults | Allowed values | Validated by | Stored in | Open questions
```

Required facts:

- `Configuration sets Parameter`;
- `Rule validates Configuration`;
- `Storage stores Configuration` if persistent.

### 9.5. Extension Points Register

```text
ID | Name | Kind | Purpose | Extension contract | Allowed extensions | Forbidden extensions | Affected layers | Open questions
```

Required facts:

- `ExtensionPoint requires Interface`;
- `ExtensionPoint constrained_by Rule`;
- `ExtensionPoint affects View / Transformation / Layer`.

## 10. Representation registers

### 10.1. Views Register

```text
ID | Name | Viewpoint | Audience | Source elements | Source relations | Output format | Represents | Open questions
```

Required facts:

- `View conforms_to Viewpoint`;
- `View represents ModelElement / StructuredFact`;
- `Transformation produces View` when generated.

### 10.2. Viewpoints Register

```text
ID | Name | Stakeholder | Concern | Allowed views | Relevant element types | Correspondence rules | Open questions
```

Required facts:

- `Viewpoint frames View`;
- `Stakeholder has Concern` if Stakeholder/Concern are modeled.

### 10.3. Transformations Register

```text
ID | Name | Input elements | Input relations | Output | Rules | Validation before | Validation after | Open questions
```

Required facts:

- `Transformation reads Model / StructuredFact`;
- `Transformation produces View / SDD / TaskList / TestPlan / CodexContext`.

### 10.4. Validation Rules Register

```text
ID | Name | Applies to | Condition | Expected result | Severity | Violation message | Blocks transformation | Open questions
```

Required facts:

- `ValidationRule checks ElementType / RelationType / StructuredFact / View`;
- `ValidationRule blocks Transformation` if severity is blocker.

## 11. Verification and implementation registers

### 11.1. TestCases Register

```text
ID | Name | Target | Type | Preconditions | Steps | Expected result | Requirement gap | Status | Automation status | Open questions
```

Required facts:

- `TestCase verifies Requirement / Rule / Flow / Interface / Error / CodeArtifact`;
- `Requirement is_verified_by TestCase`;
- if clear Requirement is absent: `TestCase reveals_gap RequirementGap` and `TestCase blocked_by RequirementGap`.

Rule:

- TestCase may reveal missing or unclear Requirement, but TestCase must not become the source of expected behavior.

### 11.2. Tasks Register

```text
ID | Name | Source | Purpose | Expected output | Affected elements | Affected artifacts | Verified by | Status | Open questions
```

Required facts:

- `Task implements Requirement` or `Task resolves OpenQuestion` or `Task updates ModelElement`;
- `Task changes CodeArtifact` if implementation is involved.

### 11.3. CodeArtifacts Register

```text
ID | Name | Artifact type | Path / location | Responsibility | Implements | Changed by | Verified by | Status | Open questions
```

Required facts:

- `CodeArtifact implements Service / Module / Task / Rule / Interface / TestCase`;
- `TestCase verifies CodeArtifact` when applicable.

### 11.4. OpenQuestions Register

```text
ID | Question | Context | Source | Affected elements | Options | Status | Resolution | Opened by | Open questions
```

Required facts:

- `OpenQuestion affects ModelElement / Relation / View / Transformation`;
- `Task resolves OpenQuestion` or `Decision resolves OpenQuestion` when closed.

### 11.5. RequirementGaps Register

Назначение: отдельно фиксировать разрывы требований, найденные через нужные проверки, ревью или валидацию модели.

```text
ID | Needed check | Missing or unclear Requirement | Linked TestCase | Affected elements | Status | Resolution path | Resolution Requirement | Open questions
```

Required facts:

- `TestCase reveals_gap RequirementGap`;
- `TestCase blocked_by RequirementGap` while Requirement is absent or unclear;
- `RequirementGap affects Requirement / Rule / Flow / Error / Module / SDDSection`;
- `Requirement resolves RequirementGap` when Requirement is created or clarified.

Rule:

- RequirementGap закрывается только через созданный/уточнённый Requirement или явное решение `rejected`.

## 12. Relationship registers

### 12.1. Facts Register

Назначение: показывать все structured facts.

```text
ID | Subject | Relation | Object | Source | Status | Required | Validation status | Used in SDD | Open questions
```

Required checks:

- subject exists;
- relation type exists;
- object exists;
- source exists for important facts.

### 12.2. Traceability Matrix

Назначение: показывать цепочки от требований к задачам, коду и тестам.

```text
Requirement | Related elements | Rules | Errors | Tasks | Code artifacts | Test cases | Gaps
```

Required chains:

```text
Requirement -> TestCase
Requirement -> Task -> CodeArtifact -> TestCase
```

Desired chains:

```text
Requirement -> Module -> Service -> Entity -> DataField -> Rule -> Error -> TestCase -> Task -> CodeArtifact
```

### 12.3. SDD Coverage Matrix

Назначение: показывать, какие элементы и facts попадают в какие SDD sections.

```text
SDD section | Source element types | Source relation types | Required facts | Validation before generation | Open questions
```

## 13. Registers for first validation project

Первый проверочный проект:

- [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]]

Минимальный набор registers для первого примера:

1. Requirements Register.
2. Entities Register.
3. DataFields Register.
4. Rules Register.
5. Errors Register.
6. Flows Register.
7. Interfaces Register.
8. TestCases Register.
9. Tasks Register.
10. Facts Register.
11. Traceability Matrix.

Не нужно сразу создавать все возможные registers. Для первого примера нужно проверить минимальную цепочку.

## 14. Register validation rules

### 14.1. REG-VAL-001. Row ID must exist

Каждая строка register должна иметь ID существующего элемента или факта.

Severity: `blocker`

### 14.2. REG-VAL-002. Register row must not introduce new truth

Если строка содержит новый смысл, отсутствующий в element или fact, нужно создать element/fact или OpenQuestion.

Severity: `warning`

### 14.3. REG-VAL-003. Required relation columns must be checked

Колонки обязательных связей должны показывать ID связанного элемента или gap.

Severity: `error`

### 14.4. REG-VAL-004. Open questions must not be hidden

Неполные элементы должны иметь ссылку на OpenQuestion.

Severity: `error`

### 14.5. REG-VAL-005. Generated registers must record source

Если register создан transformation, он должен иметь `generated_from`.

Severity: `warning`

## 15. Открытые вопросы

- Где физически хранить registers: в `metamodel/`, `registers/` или рядом с проверочными примерами?
- Использовать Markdown tables или YAML/CSV для первых registers?
- Должны ли registers быть отдельными файлами для каждого проекта?
- Как фиксировать generated registers и ручные правки?
- Нужно ли создавать master Facts Register до первого validation example?
- Как не перегрузить маленькие проекты слишком большим количеством registers?

## 16. Связанные документы

### Входные документы

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Передаёт: element types и обязательные поля.
  - Используется для: определения реестров по типам элементов.
  - Ограничение: не описывает табличные views.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Передаёт: relation types.
  - Используется для: колонок required facts и relationship registers.
  - Ограничение: не задаёт форму таблиц.

- [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
  - Передаёт: форму проверяемого утверждения.
  - Используется для: Facts Register и traceability matrix.
  - Ограничение: не является register view.

### Выходные документы

- Будущий [[docs/08_digital_system_cad/metamodel/05_Controlled_Vocabulary|Controlled Vocabulary]]
  - Получает: термины registers, fields, statuses и relation names.
  - Используется для: стабилизации названий и синонимов.
  - Ограничение: не должен подменять конкретные registers.

- Будущий [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Получает: Traceability Matrix как register view.
  - Используется для: правил обязательных цепочек.
  - Ограничение: не должен описывать все registers.

## 17. История изменений

- Initial version: создана спецификация model registers как табличных views над elements и structured facts, включая core, logical, architecture, representation, verification registers, relationship registers и validation rules.
