# Digital System CAD Index

## 1. Назначение документа

`00_Digital_System_CAD_Index.md` является входной картой слоя Digital System CAD.

Документ показывает:

- зачем существует слой `docs/08_digital_system_cad/`;
- какие документы уже есть;
- какие документы являются входными;
- какие документы нужно создать дальше;
- как текущая исследовательская работа должна превращаться в рабочую метамодель цифровой системы.

> [!info] Главное
> Текущий этап — не разработка приложения и не создание metamodeling workbench. Текущий этап — сбор, формирование и структурирование информации, чтобы получить рабочую метамодель цифровой системы.

## 2. Роль слоя Digital System CAD

Слой Digital System CAD нужен для исследования и формирования инженерной модели цифровой системы.

Главная рабочая гипотеза:

```text
Digital system model = typed elements + typed relations + structured facts + validation rules + views + transformations
```

Слой должен помочь ответить:

> Можно ли выделить достаточно универсальное ядро цифровой системы для SDD, задач, тестов, Codex-контекста и будущего Digital System CAD, или цифровые системы требуют только частных доменных методик?

## 3. Границы текущего этапа

Сейчас проект делает:

- собирает методы и стандарты метамоделирования;
- уточняет понятия цифрового мира;
- переводит энциклопедию в controlled vocabulary;
- формирует кандидаты элементов модели;
- формирует кандидаты связей;
- описывает structured facts;
- готовит будущие реестры, views, SDD transformations и validation rules;
- готовит проверку на примерах.

Сейчас проект не делает:

- не разрабатывает приложение;
- не строит metamodeling workbench;
- не выбирает финальный стек реализации;
- не объявляет список элементов окончательным;
- не считает диаграммы, таблицы или SDD отдельными источниками истины.

## 4. Структура папок

```text
docs/08_digital_system_cad/
├── 00_Digital_System_CAD_Index.md
├── research/
│   └── 01_Metamodeling_Methods_And_Standards.md
├── metamodel/
│   └── 01_Metamodel_Form.md
└── validation/
```

Планируемое развитие:

```text
docs/08_digital_system_cad/
├── concepts/
├── research/
├── metamodel/
├── registers/
├── sdd/
├── validation/
└── examples/
```

Папки создаются только если они помогают упорядочить документы для Obsidian и не дублируют существующие слои базы знаний.

## 5. Входные документы

### 5.1. Главные входные документы

- [[Digital_System_CAD_Concept_for_Codex|Digital System CAD Concept]]
  - Передаёт: конечную цель, гипотезу, идею модели цифровой системы, базовые элементы и роль SDD.
  - Используется для: удержания направления исследования.
  - Ограничение: не является финальной спецификацией метамодели.

- [[Digital_System_CAD_Philosophical_Essay_for_Codex|Digital System CAD Philosophical Essay]]
  - Передаёт: жёсткие принципы model/view separation, typed relations, structured facts, Definition/Context/Source и provisional metamodel.
  - Используется для: проверки качества формулировок и запрета свободных догадок.
  - Ограничение: не является технической спецификацией.

- [[PROJECT_SCOPE|PROJECT_SCOPE]]
  - Передаёт: масштаб проекта Programming Digital Systems и связь с Digital System CAD.
  - Используется для: удержания границ.
  - Ограничение: не задаёт детальный план метамодели.

- [[TODO|TODO]]
  - Передаёт: текущий оперативный план.
  - Используется для: выбора следующих работ.
  - Ограничение: не является содержательной моделью.

### 5.2. Опорные слои базы знаний

- [[docs/05_encyclopedia/Entities|Entities]]
- [[docs/05_encyclopedia/Data|Data]]
- [[docs/05_encyclopedia/Rules|Rules]]
- [[docs/05_encyclopedia/States|States]]
- [[docs/05_encyclopedia/Events|Events]]
- [[docs/05_encyclopedia/Flows|Flows]]
- [[docs/05_encyclopedia/Storage|Storage]]
- [[docs/05_encyclopedia/Errors|Errors]]
- [[docs/05_encyclopedia/Interfaces|Interfaces]]
- [[docs/05_encyclopedia/Architecture|Architecture]]
- [[docs/05_encyclopedia/Layers|Layers]]
- [[docs/05_encyclopedia/Modules|Modules]]
- [[docs/05_encyclopedia/Models|Models]]
- [[docs/05_encyclopedia/Dependencies|Dependencies]]
- [[docs/05_encyclopedia/Configurations|Configurations]]
- [[docs/05_encyclopedia/Extension_Points|Extension Points]]

Энциклопедия используется как controlled vocabulary и источник кандидатов в элементы, свойства, relation types, validation rules и open questions.

## 6. Существующие документы слоя

### 6.1. Research

- [[docs/08_digital_system_cad/research/01_Metamodeling_Methods_And_Standards|Metamodeling Methods and Standards]]
  - Назначение: зафиксировать методы, стандарты и reference technologies метамоделирования.
  - Статус: рабочий исследовательский документ.
  - Следующее действие: использовать выводы как правила при формировании элементов, связей, views и transformations.

### 6.2. Metamodel

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
  - Назначение: задать рабочую форму описания Element Type, Element Card, Relation Type, Structured Fact, Register, View, Viewpoint, Transformation, Validation Rule, Controlled Vocabulary, Questionnaire Mapping и Traceability Rule.
  - Статус: рабочая форма сбора информации.
  - Следующее действие: создать документы конкретных кандидатов метамодели.

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Назначение: описать кандидаты типов элементов модели.
  - Статус: первый рабочий список кандидатов.
  - Следующее действие: проверить элементы на первом примере и уточнить обязательные поля.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Назначение: описать кандидаты типов связей как first-class objects.
  - Статус: первый рабочий список relation types.
  - Следующее действие: использовать relation types для формы structured facts.

- [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
  - Назначение: описать форму проверяемых утверждений модели.
  - Статус: первый рабочий вариант.
  - Следующее действие: использовать facts как основу реестров, views, SDD и трассировки.

- [[docs/08_digital_system_cad/metamodel/04_Model_Registers|Model Registers]]
  - Назначение: описать registers как табличные views над elements и structured facts.
  - Статус: первый рабочий вариант.
  - Следующее действие: использовать registers для первого validation example.

- [[docs/08_digital_system_cad/metamodel/05_Controlled_Vocabulary|Controlled Vocabulary]]
  - Назначение: стабилизировать термины, определения, синонимы, запрещённые синонимы и границы применения.
  - Статус: первый рабочий вариант.
  - Следующее действие: использовать vocabulary в traceability, SDD и Codex context.

- [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Назначение: описать обязательные цепочки трассировки между требованиями, моделью, задачами, кодом, тестами, SDD и open questions.
  - Статус: первый рабочий вариант.
  - Следующее действие: использовать traceability rules при описании SDD как transformation модели.

- [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]
  - Назначение: описать SDD как набор views и transformations из модели.
  - Статус: первый рабочий вариант.
  - Следующее действие: проверить цепочку model -> SDD на первом validation example.

### 6.3. Validation

- [[docs/08_digital_system_cad/validation/01_Python_File_Processing_Utility_Metamodel_Check|Python File Processing Utility Metamodel Check]]
  - Назначение: проверить рабочую форму метамодели на первом простом примере.
  - Статус: первый validation-документ.
  - Вывод: форма применима, draft SDD возможен, но полный technical SDD блокируется open questions.

Будущая роль:

- проверка метамодели на разных типах цифровых систем;
- фиксация слабых мест;
- сравнение универсального ядра и доменных расширений;
- проверка цепочки `анкета -> модель -> SDD -> задачи -> тесты`.

## 7. Планируемые документы metamodel

Следующие документы должны появиться в `docs/08_digital_system_cad/metamodel/`.

### 7.1. `01_Model_Elements.md`

Назначение: описать кандидаты типов элементов модели.

Статус: создан первый рабочий вариант.

Ожидаемые элементы:

- Project;
- Requirement;
- Actor;
- Scenario;
- Entity;
- DataField;
- Rule;
- State;
- Event;
- Flow;
- Storage;
- Interface;
- Integration;
- Error;
- Module;
- Layer;
- Model;
- Dependency;
- Configuration;
- ExtensionPoint;
- TestCase;
- Task;
- CodeArtifact.

Для каждого элемента нужно определить:

- Definition;
- Purpose;
- Context;
- Required fields;
- Optional fields;
- Not examples;
- Related elements;
- Required relations;
- Validation questions;
- SDD usage;
- Open questions.

### 7.2. `02_Model_Relations.md`

Назначение: описать допустимые типы связей как элементы первого класса.

Статус: создан первый рабочий вариант.

Примеры связей:

- `Project contains Requirement`;
- `Entity contains DataField`;
- `Rule validates DataField`;
- `Rule raises Error`;
- `Event triggers Flow`;
- `Event changes State`;
- `Flow transfers DataField`;
- `Storage stores Entity`;
- `Interface exposes Entity`;
- `Module provides Interface`;
- `Module depends_on Module`;
- `TestCase verifies Rule`;
- `Task implements Requirement`;
- `CodeArtifact implements Module`.

### 7.3. `03_Structured_Facts.md`

Назначение: описать форму проверяемого утверждения модели.

Статус: создан первый рабочий вариант.

Минимальная форма:

```yaml
id:
subject:
relation:
object:
source:
context:
validation_status:
open_questions:
```

### 7.4. `04_Model_Registers.md`

Назначение: описать таблицы-реестры как views модели.

Статус: создан первый рабочий вариант.

Реестры не должны быть источником истины. Они должны быть табличным представлением model elements и structured facts.

### 7.5. `05_Controlled_Vocabulary.md`

Назначение: зафиксировать термины, определения, допустимые синонимы, запрещённые синонимы и границы применения.

Статус: создан первый рабочий вариант.

Главное правило:

> Имя не является определением.

### 7.6. `06_Traceability.md`

Назначение: описать обязательные цепочки трассировки.

Статус: создан первый рабочий вариант.

Минимальная цепочка:

```text
Requirement -> Task -> CodeArtifact -> TestCase
```

Желательная цепочка:

```text
Requirement -> Module -> Service -> Entity -> DataField -> Rule -> Error -> TestCase -> Task -> CodeArtifact
```

### 7.7. `07_SDD_From_Model.md`

Назначение: описать SDD как view/transformation модели.

SDD не должен быть свободным документом, оторванным от model elements, structured facts и validation rules.

Статус: создан первый рабочий вариант.

## 8. Планируемые документы validation

### 8.1. Первый проверочный пример

Источник:

- [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]]

Нужно проверить:

- можно ли выделить elements;
- можно ли назначить ID;
- можно ли построить relations;
- можно ли получить structured facts;
- можно ли сформировать SDD;
- какие элементы оказались лишними;
- каких элементов не хватило.

### 8.2. Следующие проверочные области

- GUI-приложение;
- Excel / SVG / template-система;
- CNC / промышленная автоматизация;
- web/API или интеграционная система.

## 9. Views и transformations

Digital System CAD должен рассматривать документы, таблицы, диаграммы, анкеты и SDD как views или transformations одной модели.

Основные views:

- questionnaire view;
- register view;
- diagram view;
- SDD section view;
- task list view;
- test plan view;
- Codex context view.

Основные transformations:

- `model -> SDD`;
- `model -> task list`;
- `model -> test plan`;
- `model -> diagram`;
- `model -> Codex context`;
- `questionnaire answers -> model elements`;
- `model validation -> open questions`.

## 10. Правила работы Codex в этом слое

Codex должен:

1. Не предлагать реализацию приложения раньше формирования рабочей метамодели.
2. Не считать diagram, table, questionnaire или SDD source of truth.
3. Считать source of truth моделью: typed elements, typed relations, structured facts, validation rules.
4. Добавлять новое понятие сначала в metamodel / research / controlled vocabulary, а не сразу в реализацию.
5. Не использовать имя как определение.
6. Для важных элементов фиксировать Definition, Purpose, Context и Source.
7. Если есть неоднозначность, фиксировать Open question.
8. Создавать папки и подпапки для Obsidian, если это реально улучшает структуру документов.
9. Поддерживать Obsidian wikilinks и карты.
10. Любой будущий SDD рассматривать как view/transformation модели.

## 11. Ближайший порядок работы

1. Создать полный Facts Register для [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]].
2. Создать draft SDD для Python File Processing Utility.
3. Закрыть или явно оставить open questions, влияющие на technical requirements.
4. Проверить форму на втором примере другого типа.

## 12. Критерии готовности слоя

Слой Digital System CAD считается рабочим для текущего этапа, если:

- есть индекс слоя;
- есть рабочая форма метамодели;
- есть список кандидатов элементов;
- есть список кандидатов relations;
- есть форма structured facts;
- есть правила ID и реестров;
- есть controlled vocabulary;
- есть правила трассировки;
- SDD описан как transformation модели;
- есть хотя бы один проверочный пример;
- открытые вопросы фиксируются явно.

## 13. История изменений

- Initial version: создан индекс слоя Digital System CAD с текущей структурой, входными документами, планируемыми metamodel-документами, validation-направлением и ближайшим порядком работы.
- Updated: добавлены созданные документы [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]] и [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]].
- Updated: добавлен созданный документ [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]].
- Updated: добавлен созданный документ [[docs/08_digital_system_cad/metamodel/04_Model_Registers|Model Registers]].
- Updated: добавлен созданный документ [[docs/08_digital_system_cad/metamodel/05_Controlled_Vocabulary|Controlled Vocabulary]].
- Updated: добавлен созданный документ [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]].
- Updated: добавлен созданный документ [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]].
- Updated: добавлен первый validation-документ [[docs/08_digital_system_cad/validation/01_Python_File_Processing_Utility_Metamodel_Check|Python File Processing Utility Metamodel Check]].
