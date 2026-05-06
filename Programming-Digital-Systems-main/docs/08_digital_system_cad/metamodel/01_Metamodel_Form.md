# Metamodel Form

## 1. Назначение документа

`01_Metamodel_Form.md` описывает рабочую форму метамодели цифровой системы на текущем исследовательском этапе проекта [[Digital_System_CAD_Concept_for_Codex|Digital System CAD]].

Документ не фиксирует окончательную метамодель. Он задаёт форму, через которую можно собирать, упорядочивать, связывать и проверять информацию о цифровых системах.

> [!info] Главное
> Сейчас цель — не доказать окончательный список элементов цифрового мира, а создать рабочую форму, с помощью которой можно собирать данные и постепенно уточнять метамодель.

## 2. Правило источника правды для element types

Этот документ описывает **форму** метамодели, но не должен хранить независимый полный список element types.

Текущий рабочий источник правды для списка element types:

```text
docs/08_digital_system_cad/metamodel/01_Model_Elements.md
```

Правила версионирования и приоритета списков element types описаны в:

```text
docs/08_digital_system_cad/metamodel/00_Element_Set_Versions.md
```

Это означает:

- `Digital_System_CAD_Concept_for_Codex.md` содержит начальную концептуальную версию списка;
- `01_Metamodel_Form.md` содержит форму описания метамодели;
- `01_Model_Elements.md` содержит текущий рабочий список element types;
- другие документы должны ссылаться на текущий список, а не поддерживать собственные конкурирующие версии.

Если в документах обнаружен новый кандидат element type, он должен быть:

1. добавлен как candidate в `01_Model_Elements.md`; или
2. зафиксирован как `OpenQuestion`; или
3. отнесён к будущему profile-specific / domain extension set.

## 3. Что такое рабочая форма метамодели

Рабочая форма метамодели — это способ описывать:

- какие элементы мы видим в цифровой системе;
- какие свойства есть у этих элементов;
- какие связи существуют между элементами;
- какие структурированные факты можно утверждать о системе;
- какие проверки нужны для целостности модели;
- какие views можно получить из модели;
- какие transformations превращают модель в SDD, задачи, тесты или контекст для Codex.

Рабочая форма нужна до доказательной проверки, потому что без неё невозможно одинаково собирать информацию по разным примерам.

## 4. Базовая структура

```text
Metamodel Form
├── Element Type
├── Element Card
├── Relation Type
├── Structured Fact
├── Register
├── View
├── Viewpoint
├── Transformation
├── Validation Rule
├── Controlled Vocabulary
├── Questionnaire Mapping
└── Traceability Rule
```

## 5. Element Type

`Element Type` описывает вид объекта, который может существовать в модели цифровой системы.

Форма описания `Element Type`:

```text
Type ID:
Type name:
Status:
Layer:
Definition:
Purpose:
Description:
Context:
Typical examples:
Not examples:
Required fields:
Optional fields:
Allowed relations:
Required relations:
Validation rules:
SDD usage:
Open questions:
```

Правило:

> `Element Type` должен иметь Definition, Purpose, Context и Not examples. Имя типа не считается достаточным определением.

Текущий список element types не приводится здесь намеренно. Он ведётся в [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]].

## 6. Element Card

`Element Card` описывает конкретный элемент модели на уровне M1.

Универсальная форма:

```text
ID:
Type:
Name:
Definition:
Purpose:
Description:
Status:
Source:
Owner:
Context:
Related elements:
Used in views:
Used in SDD:
Validation status:
Open questions:
```

Минимальные статусы:

- `draft`;
- `candidate`;
- `accepted`;
- `rejected`;
- `deprecated`.

Правило:

> Конкретный элемент модели не должен появляться только как имя. Если элемент влияет на SDD, задачу, тест, диаграмму или Codex context, он должен иметь Element Card.

## 7. Relation Type

`Relation Type` описывает допустимую связь между элементами.

Связь является объектом модели первого класса. Она не должна существовать только как линия на диаграмме или неявная фраза в тексте.

Форма описания типа связи:

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

Форма конкретной связи:

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

Каноническое правило направления связи проверки:

```text
TestCase verifies Requirement
```

Обратная форма:

```text
Requirement is_verified_by TestCase
```

может использоваться только как читаемое inverse view в документах, но не как отдельная хранимая связь, если inverse relation storage не введён явно.

Если проверка нужна, но ясного Requirement нет:

```text
Source element: TEST-001
Relation: reveals_gap
Target element: RGAP-001
Required: yes
Meaning: TestCase ожидает уточнения Requirement и имеет статус pending_requirement.
```

## 8. Structured Fact

`Structured Fact` описывает проверяемое утверждение о цифровой системе.

Форма:

```text
Fact ID:
Subject element:
Relation:
Object element:
Meaning:
Source:
Context:
Validation rule:
Used in views:
Open questions:
```

Примеры:

```text
RULE-001 validates FIELD-001.
RULE-001 raises ERR-001.
TEST-001 verifies REQ-001.
TASK-001 implements REQ-001.
```

Главное правило:

> Модель должна быть не списком объектов, а сетью структурированных фактов.

## 9. Register

`Register` — табличное представление элементов, связей или structured facts.

Минимальная форма реестра element type:

```text
ID | Type | Name | Status | Purpose | Related elements | Open questions
```

Реестр не должен быть отдельным источником правды. Он является view над моделью.

## 10. View

`View` — представление части модели для конкретной задачи или пользователя.

Возможные views:

- questionnaire;
- table;
- diagram;
- tree;
- SDD section;
- task list;
- test plan;
- Codex context.

Форма описания view:

```text
View ID:
View name:
Purpose:
Audience:
Viewpoint:
Source elements:
Source relations:
Shown fields:
Hidden fields:
Grouping rules:
Sorting rules:
Validation shown:
Output format:
Open questions:
```

## 11. Viewpoint

`Viewpoint` описывает, с какой позиции рассматривается модель.

Форма:

```text
Viewpoint ID:
Name:
Stakeholder:
Concern:
Allowed views:
Relevant element types:
Relevant relation types:
Correspondence rules:
Open questions:
```

Примеры viewpoint:

- requirements viewpoint;
- architecture viewpoint;
- data viewpoint;
- testing viewpoint;
- implementation viewpoint;
- Codex context viewpoint.

## 12. Transformation

`Transformation` описывает преобразование модели в другой результат.

Примеры:

- model -> SDD;
- model -> task list;
- model -> test plan;
- model -> diagram;
- model -> Codex context.

Форма описания transformation:

```text
Transformation ID:
Name:
Input elements:
Input relations:
Output:
Rules:
Validation before transformation:
Validation after transformation:
Open questions:
```

## 13. Validation Rule

`Validation Rule` описывает проверку целостности модели.

Форма:

```text
Rule ID:
Name:
Applies to:
Condition:
Expected result:
Violation message:
Severity:
Related SDD section:
Related TestCase:
Open questions:
```

Минимальные уровни severity:

- `info`;
- `warning`;
- `error`;
- `blocker`.

## 14. Controlled Vocabulary

`Controlled Vocabulary` фиксирует допустимые термины модели и их значения.

Форма:

```text
Term ID:
Term:
Definition:
Allowed synonyms:
Forbidden synonyms:
Context:
Related element types:
Related relation types:
Open questions:
```

Главное правило:

> Имя не является определением. Важный термин должен иметь Definition, Context и границы применения.

## 15. Questionnaire Mapping

`Questionnaire Mapping` показывает, какие элементы модели создаёт или обновляет вопрос анкеты.

Форма:

```text
Question ID:
Question:
Creates element type:
Updates element type:
Creates relation:
Required answer:
Validation rule:
Target register:
Target SDD section:
Target view:
Open questions:
```

Главное правило:

> Анкета должна собирать структурированные данные для модели, а не только свободный текст.

## 16. Traceability Rule

`Traceability Rule` описывает обязательные цепочки связи.

Минимальная трассировка:

```text
Requirement -> Task -> CodeArtifact -> TestCase
```

Желательная трассировка:

```text
Requirement -> Module -> Service -> Entity -> DataField -> Rule -> Error -> TestCase -> Task -> CodeArtifact
```

Форма правила трассировки:

```text
Traceability Rule ID:
Source element type:
Required path:
Target element type:
Validation rule:
Violation severity:
Open questions:
```

## 17. Как использовать форму

Порядок работы:

1. Собрать информацию через существующие документы, анкеты или пример.
2. Выделить кандидаты в элементы модели.
3. Проверить текущий список element types в [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]].
4. Если нужного типа нет, создать OpenQuestion или candidate element type.
5. Дать каждому важному элементу Definition, Purpose, Context и Source.
6. Заполнить Element Cards.
7. Создать связи между элементами.
8. Описать Structured Facts.
9. Занести элементы в Register.
10. Проверить Validation Rules.
11. Сформировать нужные Views.
12. Проверить, можно ли получить SDD или Codex context.
13. Зафиксировать, каких элементов, связей или определений не хватило.

## 18. Что эта форма пока не решает

Форма пока не доказывает:

- что список элементов полный;
- что цифровой мир полностью поддаётся обобщению;
- что Digital System CAD можно реализовать как приложение;
- что Archi подходит как визуальный слой;
- что SDD можно генерировать полностью автоматически.

Эти вопросы должны проверяться позже на примерах.

## 19. Связанные документы

### Входные документы

- [[docs/08_digital_system_cad/metamodel/00_Element_Set_Versions|Element Set Versions]]
  - Передаёт: правило версионирования списков element types и текущий источник правды.
  - Используется для: предотвращения расхождения списков элементов между документами.
  - Ограничение: не описывает каждый element type подробно.

- [[docs/08_digital_system_cad/research/01_Metamodeling_Methods_And_Standards|Metamodeling Methods and Standards]]
  - Передаёт: методы и стандарты метамоделирования.
  - Используется для: выбора формы элементов, views, transformations и validation rules.
  - Ограничение: не задаёт конкретную метамодель цифровой системы.

- [[Digital_System_CAD_Concept_for_Codex|Digital System CAD Concept]]
  - Передаёт: начальную гипотезу и concept set.
  - Используется для: понимания, почему element types выделяются.
  - Ограничение: не является текущим полным списком element types.

- [[Digital_System_CAD_Philosophical_Essay_for_Codex|Digital System CAD Philosophical Essay]]
  - Передаёт: принципы structured facts, typed relations, definitions, views, interpretation, controlled vocabulary и provisional metamodel.
  - Используется для: ужесточения формы элемента, связи и view.
  - Ограничение: не является технической спецификацией.

### Выходные документы

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Получает: форму описания типов элементов.
  - Используется для: детализации текущего рабочего списка element types.
  - Ограничение: не должен менять правила формы без обновления этого документа.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Получает: форму описания связей.
  - Используется для: детализации допустимых отношений между элементами.
  - Ограничение: relation types должны ссылаться на element types из текущего working element set или фиксировать OpenQuestion.

- [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
  - Получает: форму Structured Fact.
  - Используется для: описания проверяемых утверждений модели.
  - Ограничение: не должен заново определять element types и relation types.

- [[docs/08_digital_system_cad/metamodel/04_Model_Registers|Model Registers]]
  - Получает: форму Register.
  - Используется для: описания табличных views над elements и facts.
  - Ограничение: registers не должны становиться source of truth.

- [[docs/08_digital_system_cad/metamodel/05_Controlled_Vocabulary|Controlled Vocabulary]]
  - Получает: форму Controlled Vocabulary.
  - Используется для: стабилизации терминов, definitions, synonyms, forbidden synonyms и контекстов применения.
  - Ограничение: не должен заменять element type и relation type specs.

- [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Получает: форму Traceability Rule.
  - Используется для: описания обязательных цепочек между Requirement, Task, CodeArtifact, TestCase и другими элементами модели.
  - Ограничение: не должен заменять facts и registers.

- [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]
  - Получает: формы View, Viewpoint, Transformation, Validation Rule и Traceability Rule.
  - Используется для: описания SDD как view/transformation модели.
  - Ограничение: не должен становиться свободным шаблоном SDD без source facts.

## 20. История изменений

- Initial version: создана рабочая форма метамодели для сбора, структурирования и проверки информации о цифровых системах.
- Updated: форма больше не содержит независимый полный список element types; текущий список вынесен в `01_Model_Elements.md`, а правило версионирования — в `00_Element_Set_Versions.md`.
