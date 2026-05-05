# TODO / План сбора и формирования информации под Digital System CAD

## 1. Назначение документа

`TODO.md` фиксирует рабочий план сбора, структурирования и формирования информации для проекта [[Digital_System_CAD_Concept_for_Codex|Digital System CAD]].

Документ отвечает на три вопроса:

1. Что уже сделано.
2. Что нужно сделать дальше.
3. Какой формой пользоваться, чтобы информация постепенно превращалась в рабочую метамодель цифровой системы.

> [!info] Главное
> Текущий этап — не разработка приложения и не создание metamodeling workbench. Текущий этап — сбор и формирование информации о методах метамоделирования и цифровых системах, чтобы получить рабочую форму метамодели.

## 2. Текущее состояние

### 2.1. Уже сделано

- [x] Создан концепт [[Digital_System_CAD_Concept_for_Codex|Digital System CAD Concept]].
  - Зафиксированы конечная цель, гипотеза, базовые элементы, связи, роль SDD, роль анкет, роль таблиц, роль диаграмм, проверочные проекты и варианты архитектуры.

- [x] Обновлён [[PROJECT_SCOPE|PROJECT_SCOPE]].
  - Проект связан с целью Digital System CAD.
  - Центральная задача сформулирована как проверка универсальной метамодели цифровой системы.

- [x] Обновлён [[README|README]].
  - Вход в проект теперь начинается с концепта Digital System CAD, затем переходит к масштабу и картам.

- [x] Обновлён [[AGENTS|AGENTS]].
  - Codex должен учитывать цель Digital System CAD.
  - Добавлено правило не развивать документы как обычный учебный текст без связи с метамоделью, SDD и проверкой применимости.
  - Добавлено право создавать папки и подпапки для Obsidian, если это помогает структуре знаний.

- [x] Обновлены основные карты:
  - [[docs/00_maps/00_Documentation_Map|Documentation Map]]
  - [[docs/00_maps/00_Development_Route_Map|Development Route Map]]
  - [[docs/00_maps/00_Knowledge_Layer_Map|Knowledge Layer Map]]

- [x] Созданы основные слои базы знаний:
  - регламенты;
  - шаблоны;
  - roadmap-документы;
  - анкеты;
  - энциклопедия понятий;
  - примеры;
  - диаграммы;
  - чек-листы.

- [x] Создан первый учебный пример:
  - [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]]
  - [[docs/04_questionnaires/01_Questionnaire_System_Design_Filled_Python_File_Processing_Utility|Filled Questionnaire: Python File Processing Utility]]

- [x] Создан начальный слой Digital System CAD:
  - `docs/08_digital_system_cad/research/`
  - `docs/08_digital_system_cad/metamodel/`
  - `docs/08_digital_system_cad/validation/`

- [x] Создан исследовательский документ [[docs/08_digital_system_cad/research/01_Metamodeling_Methods_And_Standards|Metamodeling Methods and Standards]].
  - Зафиксировано, что текущий этап — изучение методов и правил метамоделирования, а не разработка workbench.

- [x] Создана рабочая форма [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]].
  - Зафиксированы формы Element Type, Element Card, Relation Type, Structured Fact, Register, View, Viewpoint, Transformation, Validation Rule, Controlled Vocabulary, Questionnaire Mapping и Traceability Rule.

- [x] Добавлено философское эссе [[Digital_System_CAD_Philosophical_Essay_for_Codex|Digital System CAD Philosophical Essay]].
  - Зафиксированы принципы: модель как сеть structured facts, relation as first-class object, names are not definitions, views are not source of truth, current metamodel is provisional.

- [x] Обновлён энциклопедический слой `docs/05_encyclopedia/` под философское эссе.
  - Во все 16 статей добавлен раздел `Интерпретация для Digital System CAD`.
  - Понятия переведены в форму кандидатов модели: Definition, Context, Not examples, Related model elements / relations, Structured facts, Validation questions и Open questions.
  - Энциклопедия теперь работает как controlled vocabulary и источник кандидатов для метамодели, а не только как учебный слой.

### 2.2. Что пока не сделано

- [x] Нет индекса слоя Digital System CAD.
- [x] Создан первый рабочий документ с описанием элементов модели и обязательными полями: `docs/08_digital_system_cad/metamodel/01_Model_Elements.md`.
- [x] Нет реестров таблиц для элементов модели.
- [ ] Нет правил стабильных ID для всех типов объектов.
- [x] Нет отдельного controlled vocabulary для терминов, определений и допустимых синонимов.
  - Создан `docs/08_digital_system_cad/metamodel/05_Controlled_Vocabulary.md`.
- [x] Нет отдельного описания structured facts как основы модели.
  - Создан `docs/08_digital_system_cad/metamodel/03_Structured_Facts.md`.
- [ ] Есть общая форма Questionnaire Mapping, но ещё не применена к существующим анкетам.
- [ ] Нет SDD-шаблонов, собираемых из модели.
- [ ] Нет полного примера SDD, собранного из модели.
- [ ] Нет проверки метамодели на нескольких разных типах цифровых систем.
- [ ] Нет исследования Archi как возможного визуального слоя или основы.

## 3. Главный рабочий вопрос

Проект постепенно должен ответить:

> Можно ли выделить универсальное ядро цифровой системы, достаточное для SDD и Digital System CAD, или цифровой мир требует только отдельных частных методик?

Рабочая гипотеза сбора информации:

```text
Анкеты -> Структурированные ответы -> Реестры -> Связи -> Модель цифровой системы
Модель цифровой системы -> SDD -> Задачи -> Код -> Тесты -> Обратная трассировка
```

## 4. Приоритеты

| Приоритет | Направление | Цель |
|---|---|---|
| P0 | Сбор исследовательской базы | Зафиксировать методы, стандарты и правила метамоделирования |
| P0 | Форма работы | Использовать рабочую форму метамодели для сбора информации |
| P0 | Карты | Отразить новый слой Digital System CAD в навигации Obsidian |
| P1 | Элементы модели | Описать элементы через рабочую форму, не объявляя их окончательными |
| P1 | Structured facts | Описать модель как сеть typed elements и typed relations |
| P1 | Controlled vocabulary | Зафиксировать термины, определения, контексты и запрет неоднозначных имён |
| P1 | Анкеты | Связать вопросы анкет с Element Card, Relation и Register |
| P1 | Реестры | Описать таблицы как views модели |
| P1 | SDD | Описать SDD как view/transformation модели |
| P1 | Энциклопедия | Уточнять понятия как кандидаты в элементы, свойства или доменные расширения |
| P2 | Проверочные проекты | Проверить метамодель на GUI, Excel/SVG/template и CNC/автоматизации |
| P2 | Archi | Исследовать Archi позже как возможный visual layer, не как текущую цель |
| P3 | Оформление | Поддерживать Obsidian-ссылки, карты и читаемость |

## 5. P0. Упорядочить слой Digital System CAD

### 5.1. Решить структуру папок

- [x] Создать начальные папки:
  - `docs/08_digital_system_cad/research/`
  - `docs/08_digital_system_cad/metamodel/`
  - `docs/08_digital_system_cad/validation/`

- [ ] Создать или утвердить папку для концептов.
  - Вариант: `docs/08_digital_system_cad/concepts/`
  - Вопрос: переносить ли текущий [[Digital_System_CAD_Concept_for_Codex|Digital System CAD Concept]] из корня или оставить как главный входной документ.

- [x] После создания папок обновить:
  - [[docs/00_maps/00_Documentation_Map|Documentation Map]]
  - [[docs/00_maps/00_Knowledge_Layer_Map|Knowledge Layer Map]]
  - [[AGENTS|AGENTS]], если появятся новые правила работы с этим слоем.

### 5.2. Создать индекс слоя

- [x] Создать `docs/08_digital_system_cad/00_Digital_System_CAD_Index.md`.
- [x] В индексе зафиксировать:
  - назначение слоя;
  - входные документы;
  - выходные документы;
  - список документов метамодели;
  - список документов проверки;
  - связь с SDD;
  - связь с roadmap, анкетами, примерами и диаграммами.

Критерий готовности: по индексу понятно, где живёт исследование Digital System CAD и какие документы нужно читать дальше.

## 6. P0. Собирать информацию через рабочую форму

На текущем этапе не нужно сразу доказывать полноту метамодели. Нужно собирать информацию в одинаковой форме, чтобы потом можно было сравнивать разные цифровые системы.

Основной документ формы:

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]

Порядок работы:

1. Выбрать источник информации:
   - концепт;
   - roadmap;
   - анкета;
   - пример;
   - стандарт метамоделирования;
   - реальная цифровая система.
2. Выделить кандидаты в `Element Type`.
3. Заполнить `Element Card`.
4. Проверить, что важный элемент имеет Definition, Purpose, Context и Source.
5. Описать возможные `Relation Type`.
6. Описать `Structured Fact`.
7. Определить, нужен ли `Register`.
8. Определить, какие `View` и `Viewpoint` нужны пользователю, Codex или SDD.
9. Описать возможные `Transformation`.
10. Описать возможные `Validation Rule`.
11. Зафиксировать открытые вопросы.
12. Не объявлять элемент универсальным, пока он не проверен на примерах.

Критерий готовности: новая информация попадает не в свободный текст, а в форму, пригодную для сравнения, проверки и дальнейшего превращения в метамодель.

## 7. P1. Сформировать кандидаты метамодели

### 7.1. Элементы модели

- [x] Создать документ `01_Model_Elements.md`.
- [x] Описать базовые элементы:
  - Project;
  - Requirement;
  - Actor;
  - Scenario;
  - Module;
  - Service;
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
  - TestCase;
  - RequirementGap;
  - Task;
  - CodeArtifact.

Для каждого элемента определить:

- назначение;
- обязательные поля;
- дополнительные поля;
- критерии полноты;
- типичные ошибки выделения;
- связанные элементы;
- место в SDD.

### 7.2. Связи модели

- [x] Создать документ `02_Model_Relations.md`.
- [x] Описать допустимые связи:
  - `Project содержит Requirement`;
  - `Requirement реализуется Module`;
  - `Requirement проверяется TestCase`;
  - `TestCase reveals_gap RequirementGap`, если проверка нужна, но нет ясного Requirement;
  - `TestCase blocked_by RequirementGap` до уточнения требования;
  - `Requirement разбивается на Task`;
  - `Module содержит Service`;
  - `Service processes / creates / updates Entity`;
  - `Service is_implemented_by CodeArtifact`;
  - `Module использует Entity`;
  - `Entity содержит DataField`;
  - `DataField проверяется Rule`;
  - `Rule при нарушении вызывает Error`;
  - `Event меняет State`;
  - `Flow передаёт Entity или DataField`;
  - `Task изменяет CodeArtifact`;
  - `CodeArtifact реализует Module`.

- [ ] Разделить связи на:
  - универсальные;
  - частые, но необязательные;
  - доменные;
  - запрещённые или подозрительные.

### 7.3. Структурированные факты

- [x] Создать документ `03_Structured_Facts.md`.
- [x] Описать правило:

```text
Model = typed elements + typed relations + definitions + constraints + traceability
```

- [x] Зафиксировать формы фактов:
  - `Rule validates DataField`;
  - `Rule raises Error`;
  - `TestCase verifies Rule`;
  - `Task implements Requirement`;
  - `CodeArtifact realizes Task`.

- [x] Описать, как facts попадают в SDD, таблицы, диаграммы и Codex context.

### 7.4. Идентификаторы и реестры

- [x] Создать документ `04_Model_Registers.md`.
- [x] Описать правила стабильных ID:
  - `REQ-001`;
  - `MOD-001`;
  - `ENT-001`;
  - `FIELD-001`;
  - `RULE-001`;
  - `ERR-001`;
  - `TEST-001`;
  - `TASK-001`;
  - `CODE-001`.

- [x] Описать минимальные табличные реестры:
  - Requirements Register;
  - Actors Register;
  - Scenarios Register;
  - Modules Register;
  - Entities Register;
  - DataFields Register;
  - Rules Register;
  - States Register;
  - Events Register;
  - Flows Register;
  - Storage Register;
  - Interfaces Register;
  - Integrations Register;
  - Errors Register;
  - TestCases Register;
  - Tasks Register;
  - CodeArtifacts Register.

### 7.5. Controlled vocabulary

- [x] Создать документ `05_Controlled_Vocabulary.md`.
- [x] Описать правила для терминов:
  - имя не является определением;
  - каждый важный термин имеет Definition;
  - термин имеет Context;
  - допустимые синонимы фиксируются явно;
  - запрещённые синонимы фиксируются явно;
  - новый термин не вводится без связи с элементом, relation или view.

### 7.6. Трассировка

- [x] Создать документ `06_Traceability.md`.
- [x] Зафиксировать минимальную трассировку:

```text
Requirement -> Task -> CodeArtifact -> TestCase
```

- [x] Зафиксировать желательную трассировку:

```text
Requirement -> Module -> Service -> Entity -> DataField -> Rule -> Error -> TestCase -> Task -> CodeArtifact
```

- [x] Описать, какие разрывы трассировки считаются ошибками модели.

Критерий готовности: можно взять один проект и описать его как набор кандидатов в элементы, связей, ID и проверяемой трассировки.

## 8. P1. Описать SDD как view/transformation модели

- [x] Создать документ `07_SDD_From_Model.md`.
- [x] Описать минимальный набор SDD-документов:
  - `spec.md`;
  - `requirements.md`;
  - `entities.md`;
  - `data-model.md`;
  - `rules.md`;
  - `states.md`;
  - `events.md`;
  - `flows.md`;
  - `storage.md`;
  - `interfaces.md`;
  - `integrations.md`;
  - `errors.md`;
  - `tests.md`;
  - `plan.md`;
  - `tasks.md`.

- [x] Для каждого SDD-документа определить:
  - из каких элементов модели он собирается;
  - какие поля обязательны;
  - какие связи должны быть проверены;
  - какие открытые вопросы допустимы;
  - какой результат должен получить Codex.

- [ ] Создать шаблон SDD для первого проверочного проекта.

Критерий готовности: SDD описан как view/transformation структурированной информации, а не как свободный документ.

## 9. P1. Применить форму к первому примеру

Первый проверочный пример: [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]].

- [x] Выделить элементы модели из существующего примера.
- [x] Создать первичные реестры для примера:
  - требования;
  - сущности;
  - поля данных;
  - правила;
  - ошибки;
  - тесты;
  - задачи.
- [x] Связать элементы между собой через ID на уровне sample facts и traceability matrix.
- [ ] Создать полный Facts Register для примера.
- [ ] Сформировать первый draft SDD из модели.
- [ ] Сравнить SDD с существующим описанием примера.
- [x] Зафиксировать, какие элементы модели оказались полезны.
- [x] Зафиксировать, какие элементы оказались лишними для простой Python-утилиты.

Критерий готовности: появляется первый рабочий пример цепочки `анкета -> структурированная информация -> модель-кандидат -> SDD -> задачи`.

## 10. P1. Переделать анкеты под сбор информации

Анкеты должны собирать не просто ответы, а данные для Element Card, Relation, Register, View и SDD.

- [ ] Уточнить [[docs/04_questionnaires/01_Questionnaire_System_Design|Questionnaire: System Design]].
  - Вопросы должны создавать или уточнять Project, Requirement, Actor, Scenario, Entity, DataField, Rule, State, Event, Flow, Storage, Error.

- [ ] Уточнить [[docs/04_questionnaires/02_Questionnaire_System_Architecture_Design|Questionnaire: System Architecture Design]].
  - Вопросы должны создавать или уточнять Module, Interface, Dependency, Integration, Layer, Model.

- [ ] Уточнить [[docs/04_questionnaires/03_Questionnaire_Technical_Requirements|Questionnaire: Technical Requirements]].
  - Вопросы должны превращать проектные решения в проверяемые Requirement и TestCase.

- [ ] Уточнить [[docs/04_questionnaires/06_Questionnaire_Implementation_Architecture|Questionnaire: Implementation Architecture]].
  - Вопросы должны связывать Module, Task, CodeArtifact и TestCase.

- [ ] Для каждой анкеты добавить поле:

```text
Создаёт / обновляет элементы модели:
```

Критерий готовности: после заполнения анкеты понятно, какие элементы, связи, реестры, views и открытые вопросы появились.

## 11. P1. Углубить энциклопедию как источник кандидатов

### 11.1. Базовые элементы проектирования системы

- [x] Углубить [[docs/05_encyclopedia/Entities|Entities]].
- [x] Углубить [[docs/05_encyclopedia/Data|Data]].
- [x] Углубить [[docs/05_encyclopedia/Rules|Rules]].
- [x] Углубить [[docs/05_encyclopedia/States|States]].
- [x] Углубить [[docs/05_encyclopedia/Events|Events]].
- [x] Углубить [[docs/05_encyclopedia/Flows|Flows]].
- [x] Углубить [[docs/05_encyclopedia/Storage|Storage]].
- [x] Углубить [[docs/05_encyclopedia/Errors|Errors]].
- [x] Углубить [[docs/05_encyclopedia/Interfaces|Interfaces]].

Для каждого документа добавить:

- является ли понятие элементом модели, свойством элемента или доменным расширением;
- какие поля нужны для реестра;
- какие связи с другими элементами обязательны;
- какие ошибки выделения встречаются чаще всего.

### 11.2. Архитектурные понятия

- [x] Углубить [[docs/05_encyclopedia/Architecture|Architecture]].
- [x] Углубить [[docs/05_encyclopedia/Layers|Layers]].
- [x] Углубить [[docs/05_encyclopedia/Modules|Modules]].
- [x] Углубить [[docs/05_encyclopedia/Models|Models]].
- [x] Углубить [[docs/05_encyclopedia/Dependencies|Dependencies]].
- [x] Углубить [[docs/05_encyclopedia/Configurations|Configurations]].
- [x] Углубить [[docs/05_encyclopedia/Extension_Points|Extension Points]].

Критерий готовности: энциклопедия становится источником кандидатов в элементы, свойства и доменные расширения.

Статус: первый проход выполнен. Следующий проход должен не добавлять общие пояснения, а извлекать из энциклопедии конкретные кандидаты в `01_Model_Elements.md`, `02_Model_Relations.md`, `03_Structured_Facts.md` и `05_Controlled_Vocabulary.md`.

## 12. P1. Уточнить roadmap как процесс сбора информации

- [ ] Уточнить [[docs/03_roadmaps/01_Roadmap_System_Design|Roadmap: System Design]].
  - Добавить выход: набор элементов логической модели.

- [ ] Уточнить [[docs/03_roadmaps/02_Roadmap_System_Architecture_Design|Roadmap: System Architecture Design]].
  - Добавить выход: архитектурные элементы и связи.

- [ ] Уточнить [[docs/03_roadmaps/03_Roadmap_Technical_Requirements|Roadmap: Technical Requirements]].
  - Добавить выход: проверяемые Requirement и TestCase.

- [ ] Уточнить [[docs/03_roadmaps/06_Roadmap_Implementation_Architecture|Roadmap: Implementation Architecture]].
  - Добавить выход: Task, CodeArtifact и связи с Module.

- [ ] Уточнить roadmap тестирования, эксплуатации, сопровождения и развития.
  - Добавить обратную трассировку к модели.

Критерий готовности: каждый roadmap-этап производит не просто текст, а структурированную информацию для рабочей формы метамодели.

## 13. P2. Проверить рабочую форму на разных системах

### 12.1. GUI-приложение

- [ ] Добавить пример GUI-приложения.
- [ ] Проверить роли, интерфейсы, состояния, события, сущности, правила и хранение.
- [ ] Зафиксировать, какие элементы модели нужны GUI-системам сверх простой утилиты.

### 12.2. Excel / SVG / template-система

- [ ] Добавить пример Excel/SVG/template-системы.
- [ ] Проверить шаблоны, данные, связи, правила рендера, экспорт и ошибки.
- [ ] Определить, нужен ли отдельный элемент `Template` или это доменное расширение.

### 12.3. CNC / промышленная автоматизация

- [ ] Добавить пример CNC или промышленной автоматизации.
- [ ] Проверить внешние системы, события, состояния, ошибки, ограничения безопасности и технические правила.
- [ ] Определить, какие элементы относятся к универсальному ядру, а какие к промышленному профилю.

### 12.4. Web или интеграционная система

- [ ] Добавить пример web/API или интеграционной системы.
- [ ] Проверить контракты интерфейсов, интеграции, форматы данных, ошибки обмена и тесты совместимости.

Критерий готовности: по нескольким примерам можно сравнить, какие элементы повторяются, а какие относятся к профилям систем.

## 14. P2. Исследовать Archi

- [ ] Создать документ `06_Archi_Research.md`.
- [ ] Проверить, какие данные Archi уже умеет хранить.
- [ ] Проверить user-defined properties.
- [ ] Проверить экспорт и импорт модели.
- [ ] Проверить возможность связать Archi-элементы с внешними ID модели.
- [ ] Проверить реалистичность плагина для анкет и таблиц.
- [ ] Сравнить варианты:
  - Archi как основа;
  - отдельное ядро + Archi как визуальный слой;
  - полностью отдельное приложение.

Критерий готовности: можно понять, полезен ли Archi как visual layer для будущей реализации. Это не текущая задача разработки.

## 15. P3. Поддерживать связность Obsidian

- [ ] Проверять, что новые документы добавлены в карты.
- [ ] Проверять, что новые папки имеют назначение.
- [ ] Проверять, что важные документы имеют входные и выходные связи.
- [ ] Поддерживать Obsidian wikilinks.
- [ ] Не создавать папки только ради визуальной аккуратности.
- [ ] Обновлять `История изменений` только при смысловых изменениях.

Критерий готовности: структура помогает исследованию, а не превращается в отдельную работу ради структуры.

## 16. Рекомендуемый следующий шаг

Следующий практический шаг:

1. Создать полный Facts Register для [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]].
2. Сформировать первый draft SDD из модели.
3. Закрыть или явно оставить open questions по CSV columns, word counting, report overwrite и empty folder behavior.
4. Проверить форму на втором примере другого типа.

## 17. Критерии успеха текущего этапа

Текущий этап считается успешным, если есть:

- рабочая форма сбора информации;
- список кандидатов в элементы модели с полями и критериями полноты;
- схема кандидатов связей между элементами;
- форма structured facts;
- controlled vocabulary для ключевых терминов;
- правила стабильных ID;
- набор реестров;
- правило превращения анкеты в структурированную информацию;
- первый SDD, собранный из модели-кандидата;
- первая проверка на Python-утилите;
- план проверки на GUI, Excel/SVG/template и CNC/автоматизации;
- предварительный список универсальных элементов и доменных расширений.

## 18. Связанные документы

### Входные документы

- [[Digital_System_CAD_Concept_for_Codex|Digital System CAD Concept]]
  - Передаёт: конечную цель, гипотезу, элементы модели, SDD и проверочные проекты.
  - Используется для: определения главного направления TODO.
  - Ограничение: не является оперативным планом.

- [[PROJECT_SCOPE|PROJECT_SCOPE]]
  - Передаёт: масштаб проекта и связь с Digital System CAD.
  - Используется для: удержания границ проекта.
  - Ограничение: не перечисляет конкретные задачи.

- [[AGENTS|AGENTS]]
  - Передаёт: правила работы Codex с документами, папками и метамоделью.
  - Используется для: безопасного изменения структуры и содержания.
  - Ограничение: не заменяет TODO.

- [[Digital_System_CAD_Philosophical_Essay_for_Codex|Digital System CAD Philosophical Essay]]
  - Передаёт: философские основания model/view separation, typed relations, definitions, structured facts и provisional metamodel.
  - Используется для: ужесточения критериев качества модели и roadmap-документов.
  - Ограничение: не является технической спецификацией.

- [[docs/00_maps/00_Documentation_Map|Documentation Map]]
  - Передаёт: текущую структуру документации.
  - Используется для: понимания, какие карты обновлять при новых папках и документах.
  - Ограничение: не задаёт порядок работ.

- [[docs/00_maps/00_Development_Route_Map|Development Route Map]]
  - Передаёт: маршрут от идеи до развития системы.
  - Используется для: связывания метамодели с проектным процессом.
  - Ограничение: не описывает элементы модели подробно.

- [[docs/00_maps/00_Knowledge_Layer_Map|Knowledge Layer Map]]
  - Передаёт: слои базы знаний.
  - Используется для: размещения нового слоя Digital System CAD.
  - Ограничение: не заменяет индекс нового слоя.

### Выходные документы

- [[docs/08_digital_system_cad/research/01_Metamodeling_Methods_And_Standards|Metamodeling Methods and Standards]]
  - Получает: место исследовательского документа по методам и стандартам.
  - Используется для: понимания правил метамоделирования.
  - Ограничение: не является ТЗ на workbench.

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]
  - Получает: задачу задать форму сбора и структурирования информации.
  - Используется для: разбора источников и будущего формирования кандидатов метамодели.
  - Ограничение: не является окончательной метамоделью.

- [[docs/08_digital_system_cad/00_Digital_System_CAD_Index|Digital System CAD Index]]
  - Получает: место нового слоя.
  - Используется для: навигации по метамодели, SDD, реестрам и проверкам.
  - Ограничение: не должен дублировать концепт.

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Получает: задачу описать элементы модели.
  - Используется для: формирования реестров, анкет и SDD.
  - Ограничение: не должен превращаться в энциклопедию всех понятий.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Получает: задачу описать typed relations как first-class objects.
  - Используется для: формирования structured facts, views, validation rules и трассировки.
  - Ограничение: не должен подменять concrete facts и реестры.

- [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]
  - Получает: задачу описать обязательные цепочки трассировки.
  - Используется для: проверки gaps между требованиями, моделью, задачами, кодом, тестами и SDD.
  - Ограничение: не должен заменять facts register.

- [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]
  - Получает: задачу описать SDD как результат модели.
  - Используется для: проверки полезности метамодели для разработки.
  - Ограничение: не должен быть свободным шаблоном SDD без связи с моделью.

## 19. История изменений

- Initial version: создан рабочий TODO-план дальнейшего развития базы знаний после расширения энциклопедического слоя.
- Updated: план переписан вокруг высшего приоритета — раскрытия содержания и развития информации.
- Updated: уточнено значение слова `углубить`: добавлять нужную информацию для понимания, а при насыщении темы развивать отдельные связанные документы.
- Updated: добавлен P1-блок по формированию проверяемой метамодели Digital System CAD и уточнён текущий фокус проекта.
- Updated: TODO полностью пересобран под новые реалии: добавлены сделанные работы, P0-этап слоя Digital System CAD, метамодель, SDD из модели, проверочные проекты и критерии успеха.
- Updated: TODO скорректирован под текущий этап сбора и формирования информации; metamodeling workbench зафиксирован как возможное будущее направление, а не текущая цель.
- Updated: TODO усилен выводами философского эссе: structured facts, first-class relations, controlled vocabulary и Definition/Context для важных элементов.
- Updated: отмечен выполненный первый проход по `docs/05_encyclopedia/`: все 16 статей получили раздел `Интерпретация для Digital System CAD`.
- Updated: создан и отмечен индекс слоя `docs/08_digital_system_cad/00_Digital_System_CAD_Index.md`.
- Updated: созданы и отмечены первые рабочие документы `01_Model_Elements.md` и `02_Model_Relations.md`.
- Updated: создан и отмечен документ `03_Structured_Facts.md`.
- Updated: создан и отмечен документ `04_Model_Registers.md`.
- Updated: создан и отмечен документ `05_Controlled_Vocabulary.md`.
- Updated: создан и отмечен документ `06_Traceability.md`.
- Updated: создан и отмечен документ `07_SDD_From_Model.md`.
- Updated: начата проверка формы на первом примере; создан `docs/08_digital_system_cad/validation/01_Python_File_Processing_Utility_Metamodel_Check.md`.
- Updated: добавлено правило Requirement / TestCase / RequirementGap: требование задаёт ожидаемое поведение, тест проверяет его, а отсутствующее или неясное требование фиксируется как RequirementGap со статусом `pending_requirement`.
- Updated: добавлено правило атомизации Entity / Module / Service / CodeArtifact: элемент классифицируется по роли в слое модели, а не по имени; спорные имена раскладываются на связанные элементы.
