# Link Audit: Digital System CAD

## 1. Назначение документа

`02_Link_Audit_Digital_System_CAD.md` фиксирует проверку ссылок и навигации после добавления новых документов слоя Digital System CAD.

Документ нужен, чтобы новые документы не остались изолированными и чтобы Codex понимал, какие файлы теперь входят в рабочий маршрут метамодели.

> [!info] Главное
> Новые документы должны быть связаны через центральный индекс слоя, правила element set и агентные инструкции. Большие документы нельзя перезаписывать массово без полной проверки содержимого.

## 2. Проверенные новые документы

### 2.1. Element Set Versions

Документ:

- [[docs/08_digital_system_cad/metamodel/00_Element_Set_Versions|Element Set Versions]]

Статус: создан и подключён к центральному индексу.

Назначение:

- фиксирует версии element set;
- определяет `01_Model_Elements.md` как текущий источник правды для element types;
- вводит active safety profile `v0.2-safety`;
- задаёт правила для Codex при конфликте списков элементов.

### 2.2. Safety as Model Layer

Документ:

- [[docs/08_digital_system_cad/metamodel/08_Safety_As_Model_Layer|Safety as Model Layer]]

Статус: создан и подключён к центральному индексу.

Назначение:

- фиксирует safety как часть модели, а не внешний стоп-фактор;
- описывает SafetyRequirement, SafetyRule, CriticalEvent, FailsafeState, SafetyError, SafetyTestCase, SafetyGap, SafetyGate и ForbiddenBehavior;
- задаёт правило `block unsafe paths, allow safe work`;
- задаёт P0 safety tests как приоритетный тестовый слой.

### 2.3. AGENTS override

Документ:

- [[AGENTS.override|AGENTS override]]

Статус: создан и подключён к центральному индексу.

Назначение:

- дополняет `AGENTS.md` правилами для safety-relevant systems;
- требует читать `08_Safety_As_Model_Layer.md` перед работой с safety-relevant content;
- запрещает превращать SafetyGap в полный стоп проекта;
- требует блокировать только unsafe execution paths.

## 3. Обновлённые документы

### 3.1. Metamodel Form

Документ:

- [[docs/08_digital_system_cad/metamodel/01_Metamodel_Form|Metamodel Form]]

Что обновлено:

- удалён независимый полный список element types;
- добавлена ссылка на [[docs/08_digital_system_cad/metamodel/00_Element_Set_Versions|Element Set Versions]];
- зафиксировано, что текущий список element types находится в [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]];
- добавлено правило, что новый element type должен попадать в `01_Model_Elements.md`, OpenQuestion или future profile.

### 3.2. Element Set Versions

Документ:

- [[docs/08_digital_system_cad/metamodel/00_Element_Set_Versions|Element Set Versions]]

Что обновлено:

- добавлен active safety profile `v0.2-safety`;
- добавлена ссылка на [[docs/08_digital_system_cad/metamodel/08_Safety_As_Model_Layer|Safety as Model Layer]];
- добавлены Codex rules для safety-relevant systems.

### 3.3. Digital System CAD Index

Документ:

- [[docs/08_digital_system_cad/00_Digital_System_CAD_Index|Digital System CAD Index]]

Что обновлено:

- добавлены новые документы metamodel layer;
- добавлена ссылка на [[AGENTS.override|AGENTS override]];
- добавлены разделы `Element set and form`, `Relations and facts`, `Views, vocabulary, traceability and SDD`, `Safety profile`;
- зафиксирован порядок источников правды;
- добавлен список следующих безопасных обновлений ссылок.

## 4. Текущий маршрут чтения для Codex

Для обычной работы с Digital System CAD:

```text
PROJECT_SCOPE.md
-> Digital_System_CAD_Concept_for_Codex.md
-> Digital_System_CAD_Philosophical_Essay_for_Codex.md
-> AGENTS.md
-> docs/08_digital_system_cad/00_Digital_System_CAD_Index.md
-> docs/08_digital_system_cad/metamodel/00_Element_Set_Versions.md
-> docs/08_digital_system_cad/metamodel/01_Metamodel_Form.md
-> docs/08_digital_system_cad/metamodel/01_Model_Elements.md
-> docs/08_digital_system_cad/metamodel/02_Model_Relations.md
```

Для safety-relevant systems дополнительно:

```text
AGENTS.override.md
-> docs/08_digital_system_cad/metamodel/08_Safety_As_Model_Layer.md
```

## 5. Проверка изоляции новых документов

Новые документы больше не являются изолированными, потому что:

- `00_Element_Set_Versions.md` связан с `01_Metamodel_Form.md` и `00_Digital_System_CAD_Index.md`;
- `08_Safety_As_Model_Layer.md` связан с `00_Element_Set_Versions.md`, `00_Digital_System_CAD_Index.md` и `AGENTS.override.md`;
- `AGENTS.override.md` связан через `00_Digital_System_CAD_Index.md` и ссылается на `08_Safety_As_Model_Layer.md`.

## 6. Документы, требующие следующего точечного обновления

Эти документы желательно обновить позже точечно, когда можно безопасно получить и проверить полное содержимое файла:

### 6.1. TODO

Документ:

- [[TODO|TODO]]

Нужные изменения:

- добавить `00_Element_Set_Versions.md` в выполненные работы;
- добавить `08_Safety_As_Model_Layer.md` в выполненные работы;
- добавить `AGENTS.override.md` в выполненные работы;
- исправить строки вида `Нет ...`, если задача уже закрыта;
- добавить пункт о проверке safety profile на safety-relevant validation example.

### 6.2. Documentation Map

Документ:

- [[docs/00_maps/00_Documentation_Map|Documentation Map]]

Нужные изменения:

- добавить `AGENTS.override.md` в агентный слой;
- добавить `00_Element_Set_Versions.md` и `08_Safety_As_Model_Layer.md` в слой Digital System CAD;
- обновить текст общей структуры, если карта должна перечислять все файлы.

### 6.3. Knowledge Layer Map

Документ:

- [[docs/00_maps/00_Knowledge_Layer_Map|Knowledge Layer Map]]

Нужные изменения:

- добавить safety profile как часть Digital System CAD knowledge layer;
- связать safety profile с traceability, tests, SDD и Codex context.

### 6.4. Traceability

Документ:

- [[docs/08_digital_system_cad/metamodel/06_Traceability|Traceability]]

Нужные изменения:

- добавить safety traceability chain:

```text
SafetyRequirement -> SafetyRule -> CriticalEvent -> FailsafeState -> SafetyError -> SafetyTestCase -> Task -> CodeArtifact
```

- добавить правило, что SafetyGap блокирует unsafe task, но не safe work.

### 6.5. SDD From Model

Документ:

- [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]

Нужные изменения:

- добавить SDD safety section для safety-relevant systems;
- добавить transformation `Model slice -> Safety-aware Codex Task Pack`;
- добавить P0 safety tests в test plan generation.

## 7. Ограничение текущей проверки

На текущем шаге не выполнена полная автоматическая проверка всех Obsidian wikilinks во всём репозитории.

Причина:

- GitHub connector позволяет безопасно читать и заменять отдельные файлы;
- большие документы иногда возвращаются в усечённом виде;
- массовая замена больших файлов без полного содержимого может повредить документы.

Поэтому на этом этапе выполнена безопасная навигационная синхронизация:

- центральный индекс обновлён;
- новые документы связаны между собой;
- источник правды для element types зафиксирован;
- safety profile включён в метамодельный слой;
- оставшиеся обновления перечислены как controlled follow-up tasks.

## 8. Правило дальнейшего обновления ссылок

При дальнейшем обновлении ссылок нужно соблюдать правило:

```text
Не перезаписывать большой документ, если нет полного текста файла.
```

Безопасный порядок:

1. Прочитать полный файл локально или через Codex/Git.
2. Найти все wikilinks.
3. Проверить существование target-файлов.
4. Обновить только нужные разделы.
5. Проверить diff.
6. Сделать commit.

## 9. История изменений

- Initial version: создан отчёт проверки ссылок после добавления Element Set Versions, Safety as Model Layer и AGENTS override.
