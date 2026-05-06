# Digital System CAD Index

## 1. Назначение документа

`00_Digital_System_CAD_Index.md` является входной картой слоя Digital System CAD.

Документ показывает:

- зачем существует слой `docs/08_digital_system_cad/`;
- какие документы уже есть;
- какие документы являются входными;
- какие документы нужно читать Codex и человеку;
- как текущая исследовательская работа должна превращаться в рабочую метамодель цифровой системы;
- где находятся актуальные документы по element types, relation types, safety profile, traceability и SDD transformation.

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
- описывает registers как views модели;
- описывает traceability rules;
- описывает SDD как transformation модели;
- описывает safety как model layer / active profile;
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
│   ├── 00_Element_Set_Versions.md
│   ├── 01_Metamodel_Form.md
│   ├── 01_Model_Elements.md
│   ├── 02_Model_Relations.md
│   ├── 03_Structured_Facts.md
│   ├── 04_Model_Registers.md
│   ├── 05_Controlled_Vocabulary.md
│   ├── 06_Traceability.md
│   ├── 07_SDD_From_Model.md
│   └── 08_Safety_As_Model_Layer.md
└── validation/
    └── 01_Python_File_Processing_Utility_Metamodel_Check.md
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

## 5. Главные входные документы

- [[PROJECT_SCOPE|PROJECT_SCOPE]]
  - Передаёт: масштаб проекта Programming Digital Systems и связь с Digital System CAD.
  - Используется для: удержания границ.
  - Ограничение: не задаёт детальный план метамодели.

- [[Digital_System_CAD_Concept_for_Codex|Digital System CAD Concept]]
  - Передаёт: конечную цель, гипотезу, идею модели цифровой системы, базовые элементы и роль SDD.
  - Используется для: удержания направления исследования.
  - Ограничение: не является финальной спецификацией метамодели.

- [[Digital_System_CAD_Philosophical_Essay_for_Codex|Digital System CAD Philosophical Essay]]
  - Передаёт: принципы model/view separation, typed relations, structured facts, Definition/Context/Source и provisional metamodel.
  - Используется для: проверки качества формулировок и запрета свободных догадок.
  - Ограничение: не является технической спецификацией.

- [[AGENTS|AGENTS]]
  - Передаёт: общие правила работы AI-агента с репозиторием.
  - Используется для: сохранения структуры, масштаба и связи с Digital System CAD.
  - Ограничение: не заменяет документы конкретного слоя.

- [[AGENTS.override|AGENTS override]]
  - Передаёт: дополнительные правила для safety-relevant systems.
  - Используется для: применения `Safety as Model Layer` в Codex workflow.
  - Ограничение: не заменяет основной `AGENTS.md`, а дополняет его.

- [[TODO|TODO]]
  - Передаёт: текущий оперативный план.
  - Используется для: выбора следующих работ.
  - Ограничение: не является содержательной моделью.

## 6. Опорные слои базы знаний

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

Если термин из энциклопедии конфликтует с рабочей метамоделью, приоритет имеет рабочий metamodel layer, а конфликт фиксируется как OpenQuestion.

## 7. Документы Research

- [[docs/08_digital_system_cad/research/01_Metamodeling_Methods_And_Standards|Metamodeling Methods and Standards]]
  - Назначение: зафиксировать методы, стандарты и reference technologies метамоделирования.
  - Статус: рабочий исследовательский документ.
  - Следующее действие: использовать выводы как правила при формировании элементов, связей, views и transformations.

## 8. Документы Metamodel

### 8.1. Element set and form

- [[docs/08_digital_system_cad/metamodel/00_Element_Set_Versions|Element Set Versions]]
  - Назначение: зафиксировать правило версионирования element types и определить текущий источник правды.
  - Статус: рабочий документ согласования списков element types.
  - Передаёт: v0.1 concept set, v0.2 working metamodel candidate set, v0.2-safety active profile, v0.3 future profiles.
  - Ограничение: не описывает каждый element type подробно.

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
  - Назначение: задать рабочую форму описания Element Type, Element Card, Relation Type, Structured Fact, Register, View, Viewpoint, Transformation, Validation Rule, Controlled Vocabulary, Questionnaire Mapping и Traceability Rule.
  - Статус: рабочая форма сбора информации.
  - Ограничение: не хранит собственный независимый список element types.

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Назначение: описать текущие кандидаты типов элементов модели.
  - Статус: текущий рабочий источник правды для element types.
  - Следующее действие: проверять элементы на примерах и уточнять обязательные поля.

### 8.2. Relations and facts

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Назначение: описать кандидаты типов связей как first-class objects.
  - Статус: первый рабочий список relation types.
  - Следующее действие: использовать relation types для structured facts и traceability.

- [[docs/08_digital_system_cad/metamodel/03_Structured_Facts|Structured Facts]]
  - Назначение: описать форму проверяемых утверждений модели.
  - Статус: первый рабочий вариант.
  - Следующее действие: использовать facts как основу registers, views, SDD и трассировки.

### 8.3. Views, vocabulary, traceability and SDD

- [[docs/08_digital_system_cad/metamodel/04_Model_Registers|Model Registers]]
  - Назначение: описать registers как табличные views над elements и structured facts.
  - Статус: первый рабочий вариант.
  - Следующее действие: использовать registers для validation examples.

- [[docs/08_digital_system_cad/metamodel/05_Controlled_Vocabulary|Controlled Vocabulary]]
  - Назначение: стабилизировать термины, определения, синонимы, запрещённые синонимы и границы применения.
  - Статус: первый рабочий вариант.
  - Следующее действие: использовать vocabulary в traceability, SDD и Codex context.

- [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Назначение: описать обязательные цепочки трассировки между требованиями, моделью, задачами, кодом, тестами, SDD и open questions.
  - Статус: первый рабочий вариант.
  - Следующее действие: расширить traceability правилами safety profile.

- [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]
  - Назначение: описать SDD как набор views и transformations из модели.
  - Статус: первый рабочий вариант.
  - Следующее действие: проверить цепочку model -> SDD на validation example.

### 8.4. Safety profile

- [[docs/08_digital_system_cad/metamodel/08_Safety_As_Model_Layer|Safety as Model Layer]]
  - Назначение: описать safety как часть модели, а не как внешний стоп-фактор.
  - Статус: active profile для safety-relevant systems.
  - Передаёт: SafetyRequirement, SafetyRule, CriticalEvent, FailsafeState, SafetyError, SafetyTestCase, SafetyGap, SafetyGate, ForbiddenBehavior, P0 safety tests.
  - Главное правило: SafetyGap блокирует только unsafe execution paths и разрешает safe work продолжаться.
  - Ограничение: safety profile не заменяет доменные safety standards, но задаёт рабочую форму модели и Codex workflow.

## 9. Документы Validation

- [[docs/08_digital_system_cad/validation/01_Python_File_Processing_Utility_Metamodel_Check|Python File Processing Utility Metamodel Check]]
  - Назначение: проверить рабочую форму метамодели на первом простом примере.
  - Статус: первый validation-документ.
  - Вывод: форма применима, draft SDD возможен, но полный technical SDD блокируется open questions.

Будущая роль validation:

- проверка метамодели на разных типах цифровых систем;
- фиксация слабых мест;
- сравнение универсального ядра и доменных расширений;
- проверка цепочки `анкета -> модель -> SDD -> задачи -> тесты`;
- проверка safety profile на safety-relevant systems.

## 10. Текущий источник правды

Для текущей работы действует такой порядок:

```text
PROJECT_SCOPE.md
-> Digital_System_CAD_Concept_for_Codex.md
-> 00_Element_Set_Versions.md
-> 01_Metamodel_Form.md
-> 01_Model_Elements.md
-> 02_Model_Relations.md
-> 08_Safety_As_Model_Layer.md, если система safety-relevant
-> 03_Structured_Facts.md
-> 04_Model_Registers.md
-> 05_Controlled_Vocabulary.md
-> 06_Traceability.md
-> 07_SDD_From_Model.md
-> validation examples
```

Правило:

> Если документ содержит старый или укороченный список element types, он должен считаться concept / historical / explanatory list, а не текущим рабочим источником правды.

## 11. Следующие обновления ссылок

При следующей безопасной ревизии нужно проверить необходимость точечного обновления:

- [[TODO|TODO]]
  - Добавить `00_Element_Set_Versions.md` и `08_Safety_As_Model_Layer.md` в список сделанного.
  - Исправить старые строки вида `Нет ...`, если они уже закрыты.

- [[docs/00_maps/00_Documentation_Map|Documentation Map]]
  - Добавить ссылку на `AGENTS.override.md` и safety profile в агентный и Digital System CAD слои.

- [[docs/00_maps/00_Knowledge_Layer_Map|Knowledge Layer Map]]
  - Добавить safety profile как часть Digital System CAD knowledge layer.

- [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Добавить отдельный traceability pattern для SafetyRequirement -> SafetyRule -> SafetyTestCase -> Task -> CodeArtifact.

- [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]
  - Добавить правило, что SDD должен иметь safety section для safety-relevant systems.

## 12. История изменений

- Initial version: создан индекс слоя Digital System CAD.
- Updated: добавлены ссылки на `00_Element_Set_Versions.md`, `08_Safety_As_Model_Layer.md`, `AGENTS.override.md`, обновлена структура metamodel-документов и источник правды для element types.
