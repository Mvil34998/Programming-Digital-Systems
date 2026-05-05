# Roadmap System Design Diagrams / Диаграммы проектирования системы

## 1. Назначение документа

`01_Roadmap_System_Design_Diagrams.md` хранит диаграммы этапа проектирования системы.

Документ визуализирует, как из идеи системы выделяются граница, сущности, данные, правила, состояния, события, потоки, хранение и ошибки.

Документ не заменяет [[docs/03_roadmaps/01_Roadmap_System_Design|Roadmap: System Design]] и [[docs/04_questionnaires/01_Questionnaire_System_Design|Questionnaire: System Design]].

> [!info] Главное
> Документ хранит визуальные схемы, которые помогают читать структуру, связи и маршрут.

## 2. Связанные документы

- [[docs/03_roadmaps/01_Roadmap_System_Design|Roadmap: System Design]]
- [[docs/04_questionnaires/01_Questionnaire_System_Design|Questionnaire: System Design]]
- [[docs/05_encyclopedia/Entities|Entities]]
- [[docs/05_encyclopedia/Data|Data]]
- [[docs/05_encyclopedia/Rules|Rules]]
- [[docs/05_encyclopedia/States|States]]
- [[docs/05_encyclopedia/Events|Events]]
- [[docs/05_encyclopedia/Flows|Flows]]
- [[docs/05_encyclopedia/Storage|Storage]]
- [[docs/05_encyclopedia/Errors|Errors]]
- [[docs/07_diagrams/00_System_Map|System Map]]
- [[docs/07_diagrams/00_Development_Route_Diagrams|Development Route Diagrams]]

## 3. DG-SD-001. Последовательность проектирования системы

```mermaid
flowchart TD
    A[Идея системы] --> B[Граница системы]
    B --> C[Внешние участники]
    C --> D[Сущности]
    D --> E[Данные]
    E --> F[Правила]
    F --> G[Состояния]
    G --> H[События]
    H --> I[Потоки]
    I --> J[Хранение]
    J --> K[Ошибки]
    K --> L[Открытые вопросы]
    L --> M[Выход в архитектуру системы]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L,M type
```

## 4. DG-SD-002. Граница системы

```mermaid
flowchart TD
    A[Граница системы] --> B[Внутри системы]
    A --> C[Вне системы]
    A --> D[Внешние участники]
    A --> E[Внешние источники данных]
    A --> F[Внешние потребители результата]

    B --> B1[Что система делает сама]
    C --> C1[Что остаётся ручным или внешним]
    D --> D1[Пользователь оператор внешняя система]
    E --> E1[Файлы сигналы API команды]
    F --> F1[Отчёт интерфейс файл действие]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,B1,C1,D1,E1,F1 type
```

## 5. DG-SD-003. Классификация сущностей

```mermaid
flowchart TD
    A[Сущности] --> B[Предметные сущности]
    A --> C[Информационные сущности]
    A --> D[Системные сущности]
    A --> E[Интерфейсные сущности]
    A --> F[Результирующие сущности]

    B --> B1[Пример: деталь инструмент датчик]
    C --> C1[Пример: запись модель DTO]
    D --> D1[Пример: сервис модуль обработчик]
    E --> E1[Пример: кнопка команда API]
    F --> F1[Пример: отчёт файл сообщение]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,B1,C1,D1,E1,F1 type
```

Правило чтения диаграммы: верхний уровень содержит виды сущностей, нижний уровень содержит примеры внутри вида.

## 6. DG-SD-004. Данные и правила

```mermaid
flowchart TD
    A[Данные] --> B[Входные данные]
    A --> C[Внутренние данные]
    A --> D[Хранимые данные]
    A --> E[Выходные данные]
    A --> F[Конфигурационные данные]
    A --> G[Диагностические данные]

    B --> H[Правила проверки]
    C --> I[Правила обработки]
    D --> J[Правила хранения]
    E --> K[Правила результата]
    F --> L[Правила конфигурации]
    G --> M[Правила логирования]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L,M type
```

## 7. DG-SD-005. Состояния, события и потоки

```mermaid
flowchart TD
    A[Состояние] --> B[Допустимое событие]
    B --> C[Реакция системы]
    C --> D[Поток данных или команд]
    D --> E[Новое состояние]
    D --> F[Ошибка]
    F --> G[Реакция на ошибку]
    G --> E

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G type
```

## 8. DG-SD-006. Хранение и ошибки

```mermaid
flowchart TD
    A[Хранимые данные] --> B[Назначение хранения]
    B --> C[Жизненный цикл]
    C --> D[Правила обновления]
    D --> E[Правила архивирования]
    E --> F[Требования к целостности]
    F --> G[Ошибки хранения]
    G --> H[Реакция системы]
    H --> I[Лог или сообщение]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I type
```

## 9. DG-SD-007. Выходные данные этапа

```mermaid
flowchart TD
    A[Проектирование системы завершено] --> B[Граница системы]
    A --> C[Сущности]
    A --> D[Данные]
    A --> E[Правила]
    A --> F[Состояния]
    A --> G[События]
    A --> H[Потоки]
    A --> I[Хранение]
    A --> J[Ошибки]
    A --> K[Открытые вопросы]
    B --> L[Проектирование архитектуры системы]
    C --> L
    D --> L
    E --> L
    F --> L
    G --> L
    H --> L
    I --> L
    J --> L

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L type
```

## 10. Следующий шаг

После просмотра диаграмм необходимо вернуться к связанному roadmap-документу или карте, где эти схемы применяются.

## 11. История изменений

- Initial version: созданы диаграммы этапа проектирования системы.
- Updated: документ приведён к единому визуальному формату проекта.
