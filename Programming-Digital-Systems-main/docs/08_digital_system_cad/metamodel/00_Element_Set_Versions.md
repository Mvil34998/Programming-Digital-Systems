# Element Set Versions

## 1. Назначение документа

`00_Element_Set_Versions.md` фиксирует правило согласования списков элементов рабочей метамодели Digital System CAD.

Документ нужен, чтобы разные документы проекта не содержали конкурирующие списки element types и не создавали путаницу для пользователя, Codex и будущей SDD-генерации.

> [!info] Главное
> Один и тот же список элементов не должен вручную дублироваться во всех документах. Документы могут ссылаться на разные версии набора элементов, но текущий рабочий источник правды должен быть один.

## 2. Проблема, которую решает документ

В проекте появились разные списки элементов:

- начальный концептуальный список в `Digital_System_CAD_Concept_for_Codex.md`;
- краткий список кандидатов в `01_Metamodel_Form.md`;
- расширенный рабочий список в `01_Model_Elements.md`;
- отдельные уточнения в `TODO.md`, энциклопедии и relation-документах.

Это нормально для исследовательского этапа, но без правила версионирования возникает риск:

- Codex не понимает, какой список считать главным;
- старые документы начинают конфликтовать с новой метамоделью;
- один тип элемента появляется в одном документе, но отсутствует в другом;
- новые relation types ссылаются на element types, которых нет в старом списке;
- SDD и анкеты могут строиться на разных наборах элементов.

## 3. Правило источника правды

Текущий рабочий источник правды для element types:

```text
Programming-Digital-Systems-main/docs/08_digital_system_cad/metamodel/01_Model_Elements.md
```

`01_Model_Elements.md` содержит актуальный рабочий список кандидатов element types и их формы описания.

Другие документы не должны поддерживать собственный независимый полный список element types.

Они могут:

- ссылаться на `01_Model_Elements.md`;
- показывать укороченный список для объяснения;
- описывать историческую или концептуальную версию списка;
- явно указывать, что список не является текущим источником правды.

## 4. Версии набора элементов

### 4.1. Element Set v0.1 — Concept Set

Статус: historical / concept baseline.

Источник:

```text
Digital_System_CAD_Concept_for_Codex.md
```

Назначение:

- показать первичную гипотезу проекта;
- объяснить, что цифровая система может описываться через ограниченный набор повторяющихся элементов;
- дать начальный список для исследования.

Характер списка:

```text
Project
Requirement
Actor
Scenario
Module
Entity
DataField
Rule
State
Event
Flow
Storage
Interface
Integration
Error
TestCase
Task
CodeArtifact
```

Правило использования:

> v0.1 используется как историческая концептуальная основа, но не должен считаться текущим полным списком element types.

### 4.2. Element Set v0.2 — Working Metamodel Candidate Set

Статус: current working source of truth.

Источник:

```text
docs/08_digital_system_cad/metamodel/01_Model_Elements.md
```

Назначение:

- описать текущие кандидаты element types;
- разделить уровни M2 / M1 / M0;
- дать каждому типу Definition, Purpose, Context, Not examples, Required fields, relations, validation questions и SDD usage;
- устранить смешивание Entity / Module / Service / CodeArtifact;
- подготовить основу для registers, structured facts, traceability и SDD.

Правило использования:

> Если в другом документе список элементов отличается от `01_Model_Elements.md`, приоритет имеет `01_Model_Elements.md`, если явно не указано, что документ описывает старую или частную версию.

### 4.3. Element Set v0.2-safety — Safety Profile over Working Set

Статус: active profile / safety viewpoint.

Источник:

```text
docs/08_digital_system_cad/metamodel/08_Safety_As_Model_Layer.md
```

Назначение:

- включить safety в модель как часть системы, а не как внешний запрет;
- описывать safety через специализации существующих element types;
- дать Codex правило: safety tests имеют приоритет, но SafetyGap не останавливает всю разработку;
- блокировать только unsafe execution paths, разрешая safe work продолжаться.

Safety profile не вводит отдельную финальную safety-метамодель. Он накладывается на working element set:

```text
SafetyRequirement -> Requirement
SafetyRule -> Rule
CriticalEvent -> Event
FailsafeState -> State
SafetyError -> Error
SafetyTestCase -> TestCase
SafetyValidationRule -> ValidationRule
SafetyGap -> RequirementGap / OpenQuestion
SafetyGate -> ValidationRule / Governance element
ForbiddenBehavior -> Rule / Constraint
```

Правило использования:

> Safety profile является активным профилем для safety-relevant systems. Он не должен раздувать universal core, но должен быть обязательным viewpoint, если система может создавать опасные физические, финансовые, медицинские, инфраструктурные или эксплуатационные последствия.

### 4.4. Element Set v0.3 — Future Profile / Domain Extension Set

Статус: future / not yet approved.

Назначение:

- выделить доменные расширения, которые не должны входить в универсальное ядро;
- описать профили для GUI, web, embedded, PLC, CNC/CAM, API, storage, integration, safety и Codex workflow;
- отделить универсальные element types от profile-specific element types.

Примеры возможных profile-specific кандидатов:

```text
ExternalTechnicalEnvironment
ExternalResource
ExternalSystem
FileSystem
NetworkShare
DatabaseServer
MessageBroker
UIControl
Endpoint
Device
PLCBlock
NCProgram
Toolpath
SafetyRequirement
SafetyRule
SafetyGate
SafetyGap
ForbiddenBehavior
```

Правило использования:

> v0.3 нельзя считать частью универсального ядра, пока элементы не проверены на нескольких типах цифровых систем. Safety profile может использовать специализации раньше, но должен ссылаться на базовые element types.

## 5. Приоритет при конфликте документов

Если документы расходятся, применяется такой приоритет:

```text
1. PROJECT_SCOPE.md
   - масштаб и цель проекта.

2. Digital_System_CAD_Concept_for_Codex.md
   - конечная гипотеза и смысл проекта.

3. 00_Element_Set_Versions.md
   - правило версионирования и приоритет списков элементов.

4. 01_Metamodel_Form.md
   - форма описания элементов, связей, views, transformations и validation rules.

5. 01_Model_Elements.md
   - текущий рабочий список element types.

6. 02_Model_Relations.md
   - текущий рабочий список relation types.

7. 08_Safety_As_Model_Layer.md
   - safety profile, safety viewpoint, SafetyGap, SafetyGate и P0 safety tests.

8. Controlled Vocabulary
   - термины, definitions, synonyms, forbidden synonyms и контексты.

9. Roadmaps / Questionnaires / Encyclopedia / Examples
   - источники применения, обучения, наполнения и проверки.
```

## 6. Правила для Codex

Codex должен соблюдать следующие правила:

1. Не копировать полный список element types в каждый документ.
2. При необходимости ссылаться на `01_Model_Elements.md` как на текущий рабочий список.
3. Если документ содержит старый список, помечать его как initial / historical / concept set.
4. Если найден новый кандидат element type, сначала добавить его как candidate в `01_Model_Elements.md` или как open question.
5. Не считать новый element type частью универсального ядра без проверки на примерах.
6. Если relation type ссылается на отсутствующий element type, создать OpenQuestion или обновить `01_Model_Elements.md`.
7. Не смешивать универсальное ядро и доменные расширения.
8. При конфликте между старой энциклопедической терминологией и рабочей метамоделью отдавать приоритет `01_Model_Elements.md`, но фиксировать конфликт как OpenQuestion.
9. Если система safety-relevant, применять `08_Safety_As_Model_Layer.md` как active profile.
10. SafetyGap не должен останавливать весь процесс. Он должен блокировать только unsafe execution paths и разрешать safe work.
11. P0 safety tests имеют приоритет над feature tests для safety-relevant behavior.

## 7. Связанные документы

### Входные документы

- [[Digital_System_CAD_Concept_for_Codex|Digital System CAD Concept]]
  - Передаёт: первичную гипотезу и исходный concept set.
  - Используется для: понимания, почему элементы вообще выделяются.
  - Ограничение: не является текущим полным списком element types.

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
  - Передаёт: форму описания element types и relation types.
  - Используется для: структурирования текущего списка элементов.
  - Ограничение: не должен хранить независимый полный список element types.

### Выходные документы

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Получает: правило, что именно этот документ является текущим рабочим источником правды для element types.
  - Используется для: детализации текущего набора элементов.
  - Ограничение: текущий список остаётся candidate set, а не финальной онтологией цифрового мира.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Получает: правило проверять, что source type и target type существуют в текущем working element set.
  - Используется для: согласования relation types с element types.
  - Ограничение: relation types не должны создавать скрытые element types без фиксации в `01_Model_Elements.md`.

- [[docs/08_digital_system_cad/metamodel/08_Safety_As_Model_Layer|Safety as Model Layer]]
  - Получает: правило profile-based расширения element set без раздувания universal core.
  - Используется для: safety-relevant systems, P0 safety tests, SafetyGap и SafetyGate.
  - Ограничение: safety profile не заменяет domain-specific safety engineering standards, но задаёт рабочую форму модели.

## 8. История изменений

- Initial version: создан документ версионирования наборов element types и правило выбора текущего источника правды.
- Updated: добавлен active safety profile `v0.2-safety`, связанный с `08_Safety_As_Model_Layer.md`.
