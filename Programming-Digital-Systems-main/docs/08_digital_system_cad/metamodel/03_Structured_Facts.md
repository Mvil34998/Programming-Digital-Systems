# Structured Facts

## 1. Назначение документа

`03_Structured_Facts.md` описывает форму структурированных фактов для рабочей метамодели Digital System CAD.

Structured Fact — это проверяемое утверждение о цифровой системе, построенное из typed elements и typed relations.

> [!info] Главное
> Digital System CAD должен работать не со свободным текстом и не с отдельными диаграммами, а с сетью структурированных фактов.

## 2. Базовая формула

Рабочая формула модели:

```text
Model = typed elements + typed relations + structured facts + validation rules + views + transformations
```

Минимальная форма факта:

```text
Subject element + Relation type + Object element
```

Примеры:

```text
ENT-001 contains DATA-001.
RULE-001 validates DATA-001.
RULE-001 raises ERR-001.
EVENT-001 triggers FLOW-001.
TEST-001 verifies RULE-001.
```

## 3. Что structured fact решает

Structured facts нужны для того, чтобы:

- связывать элементы модели;
- строить реестры;
- строить диаграммы как views;
- собирать SDD из модели;
- формировать задачи;
- формировать тест-планы;
- готовить Codex-readable context;
- проверять полноту модели;
- находить разрывы трассировки;
- фиксировать источники утверждений.

Без structured facts документы остаются набором хороших объяснений, но не становятся инженерной моделью.

## 4. Что не является structured fact

Structured fact не является:

- свободным предложением без ID;
- стрелкой на диаграмме без записи в модели;
- строкой таблицы без relation type;
- предположением без источника;
- названием элемента;
- комментарием автора;
- open question;
- кодовой зависимостью без модельного смысла.

Если утверждение важно, но его нельзя выразить через subject / relation / object, нужно либо уточнить элементы и relation type, либо создать OpenQuestion.

## 5. Универсальная форма факта

```yaml
id:
subject:
relation:
object:
meaning:
source:
context:
status:
required:
validation_status:
used_in_views:
used_in_sdd:
open_questions:
```

Поля:

| Поле | Назначение |
|---|---|
| `id` | стабильный ID факта |
| `subject` | исходный элемент |
| `relation` | тип связи |
| `object` | целевой элемент |
| `meaning` | смысл факта человеческим языком |
| `source` | откуда взято утверждение |
| `context` | где факт действует |
| `status` | статус факта |
| `required` | обязателен ли факт для полноты модели |
| `validation_status` | результат проверки |
| `used_in_views` | где факт отображается |
| `used_in_sdd` | в какие SDD-разделы попадает |
| `open_questions` | связанные неоднозначности |

## 6. Статусы факта

| Статус | Значение |
|---|---|
| `draft` | факт записан предварительно |
| `candidate` | факт выглядит полезным, но ещё не проверен |
| `accepted` | факт принят в текущей модели |
| `rejected` | факт отклонён |
| `deprecated` | факт устарел или заменён |
| `conflict` | факт конфликтует с другим фактом |

На текущем этапе большинство фактов будут иметь статус `candidate`.

## 7. Validation status

| Статус | Значение |
|---|---|
| `not_checked` | факт ещё не проверялся |
| `valid` | факт прошёл проверку |
| `warning` | факт неполный, но допустим временно |
| `error` | факт нарушает правило модели |
| `blocked` | факт нельзя использовать до уточнения |

## 8. ID фактов

Предварительный формат:

```text
FACT-<AREA>-<NUMBER>
```

Примеры:

```text
FACT-REQ-001
FACT-ENT-001
FACT-DATA-001
FACT-RULE-001
FACT-FLOW-001
FACT-ARCH-001
FACT-TEST-001
```

Правила:

- ID должен быть стабильным;
- ID не должен зависеть от позиции факта в документе;
- при изменении смысла факта нужно фиксировать изменение, а не молча переиспользовать старый ID;
- если факт отклонён, его ID не должен сразу переиспользоваться для другого смысла.

## 9. Базовые типы structured facts

### 9.1. Element ownership facts

Показывают владение, состав и контекст.

```yaml
id: FACT-ENT-001
subject: ENT-001
relation: contains
object: DATA-001
meaning: "Entity ENT-001 contains DataField DATA-001."
source: "docs/05_encyclopedia/Entities.md"
context: "Digital system logical model"
status: candidate
required: true
validation_status: not_checked
used_in_views:
  - entity_register
  - data_model_view
used_in_sdd:
  - entities.md
  - data-model.md
open_questions: []
```

### 9.2. Validation facts

Показывают, что правило проверяет или ограничивает элемент.

```yaml
id: FACT-RULE-001
subject: RULE-001
relation: validates
object: DATA-001
meaning: "Rule RULE-001 validates DataField DATA-001."
source: "docs/05_encyclopedia/Rules.md"
context: "Data validation"
status: candidate
required: true
validation_status: not_checked
used_in_views:
  - rules_register
  - validation_matrix
used_in_sdd:
  - rules.md
  - data-model.md
open_questions: []
```

### 9.3. Error facts

Показывают связь нарушения с ошибкой и реакцией.

```yaml
id: FACT-ERR-001
subject: RULE-001
relation: raises
object: ERR-001
meaning: "Violation of RULE-001 raises ERR-001."
source: "docs/05_encyclopedia/Errors.md"
context: "Negative scenario"
status: candidate
required: true
validation_status: not_checked
used_in_views:
  - error_register
  - negative_scenario_view
used_in_sdd:
  - errors.md
  - tests.md
open_questions: []
```

### 9.4. Behavior facts

Показывают запуск потоков, событий и переходов.

```yaml
id: FACT-FLOW-001
subject: EVENT-001
relation: triggers
object: FLOW-001
meaning: "Event EVENT-001 triggers Flow FLOW-001."
source: "docs/05_encyclopedia/Events.md"
context: "Behavior model"
status: candidate
required: true
validation_status: not_checked
used_in_views:
  - flow_diagram
  - sequence_view
used_in_sdd:
  - events.md
  - flows.md
open_questions: []
```

### 9.5. Interface facts

Показывают контракт взаимодействия.

```yaml
id: FACT-INT-001
subject: INTERFACE-001
relation: accepts
object: DATA-001
meaning: "Interface INTERFACE-001 accepts DataField DATA-001."
source: "docs/05_encyclopedia/Interfaces.md"
context: "Interface contract"
status: candidate
required: true
validation_status: not_checked
used_in_views:
  - interface_register
  - contract_view
used_in_sdd:
  - interfaces.md
open_questions: []
```

### 9.6. Architecture facts

Показывают архитектурные ответственности и зависимости.

```yaml
id: FACT-ARCH-001
subject: MODULE-001
relation: provides
object: INTERFACE-001
meaning: "Module MODULE-001 provides Interface INTERFACE-001."
source: "docs/05_encyclopedia/Modules.md"
context: "Architecture model"
status: candidate
required: true
validation_status: not_checked
used_in_views:
  - module_register
  - architecture_diagram
used_in_sdd:
  - architecture.md
  - interfaces.md
open_questions: []
```

### 9.7. Verification facts

Показывают проверку требований, правил, ошибок и артефактов.

```yaml
id: FACT-TEST-001
subject: TEST-001
relation: verifies
object: REQ-001
meaning: "TestCase TEST-001 verifies Requirement REQ-001."
source: "docs/05_encyclopedia/Rules.md"
context: "Verification model"
status: candidate
required: true
validation_status: not_checked
used_in_views:
  - traceability_matrix
  - test_plan
used_in_sdd:
  - tests.md
  - requirements.md
open_questions: []
```

### 9.8. Transformation facts

Показывают, что view или документ получен из модели.

```yaml
id: FACT-TR-001
subject: SDD-SECTION-001
relation: generated_from
object: MODEL-001
meaning: "SDD section SDD-SECTION-001 is generated from MODEL-001."
source: "docs/08_digital_system_cad/metamodel/01_Metamodel_Form.md"
context: "SDD transformation"
status: candidate
required: true
validation_status: not_checked
used_in_views:
  - sdd_generation_map
used_in_sdd:
  - spec.md
open_questions: []
```

## 10. Минимальные факты для первого SDD

Для первого проверочного SDD нужно уметь собрать минимум:

| Fact pattern | Назначение |
|---|---|
| `Project contains Requirement` | определить границы и требования |
| `Requirement references Entity` | связать требования с предметом системы |
| `Requirement is_verified_by TestCase` | закрыть проверяемость |
| `TestCase verifies Requirement` | основная машинная форма проверки требования |
| `TestCase reveals_gap RequirementGap` | зафиксировать, что проверка нужна, но Requirement отсутствует или неясен |
| `TestCase blocked_by RequirementGap` | не дать тесту подменить требование |
| `Entity contains DataField` | построить data model |
| `Rule validates DataField` | описать проверки данных |
| `Rule raises Error` | описать ошибки и реакции |
| `Event triggers Flow` | описать поведение |
| `Flow transfers DataField` | описать движение данных |
| `Storage stores Entity/DataField/Event` | описать хранение |
| `Interface accepts/returns DataField/Error` | описать контракты |
| `Module provides Interface` | описать архитектурную ответственность |
| `Module contains Service` | отделить область ответственности от исполнителя поведения |
| `Service processes Entity` | показать активную обработку данных |
| `Service creates Entity` | показать создаваемый результат |
| `Service is_implemented_by CodeArtifact` | связать поведение с реализацией без смешения слоёв |
| `Task implements Requirement` | сформировать план реализации |
| `CodeArtifact implements Module/Task` | связать код с моделью |

Если один из этих фактов нужен, но не может быть заполнен, нужно создать OpenQuestion. Если не может быть заполнена проверка из-за отсутствующего или неясного Requirement, нужно создать RequirementGap.

## 11. Факты и views

Structured facts являются источником для views.

| View | Использует facts |
|---|---|
| Entity register | `Entity contains DataField`, `Entity has State` |
| Data model table | `DataField belongs_to Entity`, `Rule validates DataField` |
| Rules matrix | `Rule validates`, `Rule constrains`, `Rule raises` |
| Flow diagram | `Event triggers Flow`, `Flow transfers`, `Flow may_raise Error` |
| Interface contract | `Interface accepts`, `Interface returns`, `Interface raises` |
| Architecture diagram | `Layer contains Module`, `Module provides Interface`, `Module depends_on Module` |
| Traceability matrix | `Requirement is_verified_by TestCase`, `Module contains Service`, `Service is_implemented_by CodeArtifact`, `TestCase reveals_gap RequirementGap`, `Task implements Requirement`, `CodeArtifact implements Task` |
| SDD sections | facts selected by viewpoint and transformation rules |

Главное правило:

> View не должен добавлять новый смысл, который отсутствует в facts. Если во view появляется новый смысл, его нужно вернуть в модель как structured fact или open question.

## 12. Факты и SDD

SDD должен собираться из facts как transformation.

Пример:

```text
facts:
  ENT-001 contains DATA-001
  RULE-001 validates DATA-001
  RULE-001 raises ERR-001

SDD sections:
  entities.md -> ENT-001
  data-model.md -> DATA-001
  rules.md -> RULE-001
  errors.md -> ERR-001
  tests.md -> expected tests for RULE-001 and ERR-001
```

Если SDD содержит утверждение, которого нет в facts, нужно:

1. создать structured fact;
2. указать source;
3. проверить relation type;
4. обновить соответствующий register/view;
5. зафиксировать open question, если факт не доказан.

## 13. Факты и Codex context

Codex context должен получать не только свободное описание задачи, но и структурированные факты:

```yaml
task:
  id: TASK-001
  implements: REQ-001
  updates:
    - CODE-001
  must_preserve:
    - RULE-001
    - INTERFACE-001
  tests:
    - TEST-001
  open_questions:
    - OQ-001
```

Так Codex сможет понимать:

- что менять;
- зачем менять;
- какие требования сохранять;
- какие правила не нарушать;
- какие тесты связаны с изменением;
- какие open questions нельзя угадывать.

## 14. Validation rules для facts

### 14.1. FACT-VAL-001. Subject must exist

Каждый `subject` должен ссылаться на существующий model element.

Severity: `blocker`

### 14.2. FACT-VAL-002. Relation type must exist

Каждый `relation` должен ссылаться на relation type из [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]] или иметь OpenQuestion о новом relation type.

Severity: `blocker`

### 14.3. FACT-VAL-003. Object must exist

Каждый `object` должен ссылаться на существующий model element.

Severity: `blocker`

### 14.4. FACT-VAL-004. Source must exist

Важный факт должен иметь source.

Severity: `error`

### 14.5. FACT-VAL-005. Required facts must be checked before transformation

Факты с `required: true` должны иметь `validation_status: valid` или documented warning перед генерацией SDD.

Severity: `error`

### 14.6. FACT-VAL-006. Views cannot be source of new truth

Если view содержит утверждение, которого нет в facts, нужно создать факт или open question.

Severity: `warning`

### 14.7. FACT-VAL-007. Conflicting facts must be explicit

Если два факта противоречат друг другу, хотя бы один из них должен получить статус `conflict` и ссылку на OpenQuestion.

Severity: `error`

## 15. Открытые вопросы

- Должен ли fact быть отдельной строкой в Markdown-таблице или YAML-блоком?
- Нужна ли отдельная папка `facts/` или facts должны жить рядом с registers?
- Как фиксировать историю изменения факта?
- Как выражать n-ary relations, где нужно больше чем subject/relation/object?
- Нужно ли вводить confidence/evidence score?
- Как отделить fact от decision?
- Какие facts обязательны до генерации первого SDD?

## 16. Связанные документы

### Входные документы

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Передаёт: допустимые subject/object element types.
  - Используется для: проверки существования элементов.
  - Ограничение: не описывает конкретные facts.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Передаёт: допустимые relation types.
  - Используется для: проверки relation в structured facts.
  - Ограничение: не описывает конкретные facts.

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
  - Передаёт: общую форму Structured Fact.
  - Используется для: структуры документа.
  - Ограничение: не задаёт минимальный набор фактов для SDD.

### Выходные документы

- Будущий [[docs/08_digital_system_cad/metamodel/04_Model_Registers|Model Registers]]
  - Получает: facts как источник табличных views.
  - Используется для: проектирования реестров.
  - Ограничение: реестры не должны становиться source of truth.

- Будущий [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Получает: facts как основу трассировки.
  - Используется для: проверки цепочек Requirement -> Task -> CodeArtifact -> TestCase.
  - Ограничение: не должен дублировать все факты.

- Будущий [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]
  - Получает: facts как источник SDD transformations.
  - Используется для: описания генерации SDD.
  - Ограничение: не должен превращаться в свободный шаблон SDD.

## 17. История изменений

- Initial version: создана форма structured facts для Digital System CAD с YAML-структурой, типами фактов, минимальными фактами для SDD, связью с views, SDD, Codex context и validation rules.
