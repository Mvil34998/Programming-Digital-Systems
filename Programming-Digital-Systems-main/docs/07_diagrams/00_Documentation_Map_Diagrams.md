# Documentation Map Diagrams / Диаграммы карты документации

## 1. Назначение документа

`00_00_Documentation_Map_Diagrams.md` хранит крупные диаграммы структуры документации проекта Programming Digital Systems.

Документ показывает, как связаны между собой уровни базы знаний: масштаб проекта, агентные правила, карты, регламенты, шаблоны, roadmap-документы, анкеты, энциклопедия, примеры и диаграммы.

Документ не заменяет [[docs/00_maps/00_Documentation_Map|Documentation Map]]. Он визуализирует её ключевые связи.

> [!info] Главное
> Документ хранит визуальные схемы, которые помогают читать структуру, связи и маршрут.

## 2. Связанные документы

### Входные документы

- [[PROJECT_SCOPE|PROJECT_SCOPE]]
  - Передаёт: масштаб проекта и идею большой связанной базы знаний.
  - Используется для: построения верхнего уровня документации.
  - Ограничение: не описывает все слои подробно.

- [[AGENTS|AGENTS]]
  - Передаёт: правила, которые должен учитывать AI-агент.
  - Используется для: связи агентного слоя с регламентами и картами.
  - Ограничение: не является картой документации.

- [[docs/00_maps/00_Documentation_Map|Documentation Map]]
  - Передаёт: полный список слоёв документации.
  - Используется для: построения диаграмм структуры.
  - Ограничение: текстовая карта не заменяет визуальные схемы.

- [[docs/00_maps/00_Knowledge_Layer_Map|Knowledge Layer Map]]
  - Передаёт: назначение каждого слоя знаний.
  - Используется для: детализации связей между слоями.
  - Ограничение: не показывает все рабочие переходы.

## 3. DG-DOC-001. Верхний уровень документации

Назначение диаграммы: показать основные слои базы знаний от масштаба проекта до диаграмм.

```mermaid
flowchart TD
    A[PROJECT_SCOPE] --> B[AGENTS]
    A --> C[Навигационные карты]
    B --> D[Регламенты]
    C --> D
    D --> E[Шаблоны]
    E --> F[Roadmap документы]
    E --> G[Анкеты]
    F --> H[Энциклопедия]
    G --> H
    H --> I[Примеры]
    F --> J[Диаграммы]
    G --> J
    H --> J
    I --> J

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J type
```

## 4. DG-DOC-002. Навигационный слой

Назначение диаграммы: показать документы, которые помогают пользователю ориентироваться в базе знаний.

```mermaid
flowchart TD
    A[Навигационный слой] --> B[Documentation Map]
    A --> C[Development Route Map]
    A --> D[Knowledge Layer Map]
    A --> E[Requirements To Toolchain Map]

    B --> F[Структура документации]
    C --> G[Маршрут разработки]
    D --> H[Слои знаний]
    E --> I[Связь требований с инструментарием]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I type
```

Связанные документы:

- [[docs/00_maps/00_Documentation_Map|Documentation Map]]
- [[docs/00_maps/00_Development_Route_Map|Development Route Map]]
- [[docs/00_maps/00_Knowledge_Layer_Map|Knowledge Layer Map]]
- [[docs/00_maps/04_Requirements_To_Toolchain_Map|Requirements To Toolchain Map]]

## 5. DG-DOC-003. Регламентный слой

Назначение диаграммы: показать, какие правила управляют созданием и изменением документов.

```mermaid
flowchart TD
    A[Регламентный слой] --> B[Documentation System Regulation]
    A --> C[Document Writing Rules]
    A --> D[Link Rules]
    A --> E[Diagram Rules]

    B --> F[Структура документации]
    C --> G[Стиль и содержание]
    D --> H[Obsidian wikilinks]
    E --> I[Mermaid диаграммы]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I type
```

Связанные документы:

- [[docs/01_regulations/Documentation_System_Regulation|Documentation System Regulation]]
- [[docs/01_regulations/Document_Writing_Rules|Document Writing Rules]]
- [[docs/01_regulations/Link_Rules|Link Rules]]
- [[docs/01_regulations/Diagram_Rules|Diagram Rules]]

## 6. DG-DOC-004. Roadmap и анкеты

Назначение диаграммы: показать парную связь roadmap-документов и анкет.

```mermaid
flowchart TD
    A[Roadmap System Design] --> B[Questionnaire System Design]
    C[Roadmap System Architecture Design] --> D[Questionnaire System Architecture Design]
    E[Roadmap Technical Requirements] --> F[Questionnaire Technical Requirements]
    G[Roadmap Toolchain Selection] --> H[Questionnaire Toolchain Selection]
    I[Roadmap Implementation Architecture] --> J[Questionnaire Implementation Architecture]
    K[Roadmap Testing] --> L[Questionnaire Testing]
    M[Roadmap Operation] --> N[Questionnaire Operation]
    O[Roadmap Maintenance] --> P[Questionnaire Maintenance]
    Q[Roadmap System Evolution] --> R[Questionnaire System Evolution]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R type
```

Правило чтения диаграммы: roadmap определяет правила этапа, анкета превращает эти правила в вопросы для конкретного проекта.

## 7. DG-DOC-005. Энциклопедический слой

Назначение диаграммы: показать ключевые понятия цифровой системы как отдельный слой знаний.

```mermaid
flowchart TD
    A[Энциклопедия] --> B[Entities]
    A --> C[Data]
    A --> D[Rules]
    A --> E[States]
    A --> F[Events]
    A --> G[Flows]
    A --> H[Storage]
    A --> I[Errors]
    A --> J[Interfaces]
    A --> K[Architecture]

    B --> L[Состав системы]
    C --> M[Информационная основа]
    D --> N[Поведение]
    E --> O[Жизненные циклы]
    F --> P[Запуск действий]
    G --> Q[Движение данных и команд]
    H --> R[Сохранение]
    I --> S[Отказы и диагностика]
    J --> T[Границы взаимодействия]
    K --> U[Организация системы]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U type
```

Связанные документы:

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

## 8. DG-DOC-006. Слой примеров

Назначение диаграммы: показать категории примеров без смешивания категорий и конкретных примеров.

```mermaid
flowchart TD
    A[Слой примеров] --> B[Скрипты автоматизации]
    A --> C[GUI приложения]
    A --> D[Web системы]
    A --> E[Embedded системы]
    A --> F[PLC системы]
    A --> G[CNC CAM системы]
    A --> H[Базы данных]
    A --> I[Интеграционные системы]

    B --> B1[Python File Processing Utility]
    C --> C1[Будущий пример: редактор шаблонов]
    D --> D1[Будущий пример: API сервис]
    E --> E1[Будущий пример: контроллер датчиков]
    F --> F1[Будущий пример: автоматический режим]
    G --> G1[Будущий пример: анализ NC программ]
    H --> H1[Будущий пример: складской учёт]
    I --> I1[Будущий пример: обмен систем]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,B1,C1,D1,E1,F1,G1,H1,I1 type
```

Связанные документы:

- [[docs/06_examples/Examples_Index|Examples Index]]
- [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]]

## 9. DG-DOC-007. Слой диаграмм

Назначение диаграммы: показать, какие документы входят в слой крупных диаграмм.

```mermaid
flowchart TD
    A[Слой диаграмм] --> B[System Map]
    A --> C[Documentation Map Diagrams]
    A --> D[Development Route Diagrams]

    B --> E[Универсальная цифровая система]
    C --> F[Структура документации]
    D --> G[Маршрут разработки]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G type
```

Связанные документы:

- [[docs/07_diagrams/00_System_Map|System Map]]
- [[docs/07_diagrams/00_Documentation_Map_Diagrams|Documentation Map Diagrams]]
- [[docs/07_diagrams/00_Development_Route_Diagrams|Development Route Diagrams]]

## 10. Правила использования диаграмм из документа

- Диаграммы используются для навигации по документации.
- Диаграммы не должны заменять текстовые определения и правила.
- Если структура документации меняется, этот документ должен обновляться вместе с [[docs/00_maps/00_Documentation_Map|Documentation Map]].
- Диаграммы должны сохранять совместимость с Obsidian Mermaid.
- Категории и примеры должны оставаться на разных уровнях графа.

## 11. Выходные связи

Этот документ должен использоваться в:

- [[docs/00_maps/00_Documentation_Map|Documentation Map]]
- [[docs/00_maps/00_Knowledge_Layer_Map|Knowledge Layer Map]]
- [[docs/07_diagrams/00_System_Map|System Map]]

## 12. Следующий шаг

После просмотра диаграмм необходимо вернуться к связанному roadmap-документу или карте, где эти схемы применяются.

## 13. История изменений

- Initial version: созданы диаграммы структуры документации, слоёв базы знаний, roadmap, анкет, энциклопедии, примеров и диаграмм.
- Updated: документ приведён к единому визуальному формату проекта.
