# Roadmap Technical Requirements Diagrams / Диаграммы технических требований

## 1. Назначение документа

`03_Roadmap_Technical_Requirements_Diagrams.md` хранит диаграммы этапа формирования технических требований.

Документ визуализирует, как проектные и архитектурные решения превращаются в проверяемые требования, критерии выполнения, способы проверки и входные данные для выбора инструментария.

Документ не заменяет [[docs/03_roadmaps/03_Roadmap_Technical_Requirements|Roadmap: Technical Requirements]] и [[docs/04_questionnaires/03_Questionnaire_Technical_Requirements|Questionnaire: Technical Requirements]].

> [!info] Главное
> Документ хранит визуальные схемы, которые помогают читать структуру, связи и маршрут.

## 2. Связанные документы

- [[docs/03_roadmaps/03_Roadmap_Technical_Requirements|Roadmap: Technical Requirements]]
- [[docs/04_questionnaires/03_Questionnaire_Technical_Requirements|Questionnaire: Technical Requirements]]
- [[docs/03_roadmaps/01_Roadmap_System_Design|Roadmap: System Design]]
- [[docs/03_roadmaps/02_Roadmap_System_Architecture_Design|Roadmap: System Architecture Design]]
- [[docs/00_maps/04_Requirements_To_Toolchain_Map|Requirements To Toolchain Map]]
- [[docs/07_diagrams/01_Roadmap_System_Design_Diagrams|Roadmap System Design Diagrams]]
- [[docs/07_diagrams/02_Roadmap_System_Architecture_Diagrams|Roadmap System Architecture Diagrams]]

## 3. DG-TR-001. Источники технических требований

```mermaid
flowchart TD
    A[Источники требований] --> B[Проектирование системы]
    A --> C[Архитектура системы]
    A --> D[Эксплуатационные ограничения]
    A --> E[Внешние ограничения]
    A --> F[Ошибки и риски]

    B --> B1[Сущности данные правила состояния события потоки хранение ошибки]
    C --> C1[Слои модули модели интерфейсы зависимости конфигурации]
    D --> D1[Запуск остановка пользователи рабочая среда]
    E --> E1[ОС оборудование стандарты заказчик]
    F --> F1[Надёжность диагностика безопасность]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,B1,C1,D1,E1,F1 type
```

## 4. DG-TR-002. Классификация технических требований

```mermaid
flowchart TD
    A[Технические требования] --> B[Данные]
    A --> C[Обработка]
    A --> D[Хранение]
    A --> E[Интерфейсы]
    A --> F[Производительность]
    A --> G[Надёжность]
    A --> H[Ошибки и диагностика]
    A --> I[Конфигурация]
    A --> J[Расширяемость]
    A --> K[Тестируемость]
    A --> L[Безопасность]
    A --> M[Окружение]
    A --> N[Эксплуатация]
    A --> O[Сопровождение]
    A --> P[Документация]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L,M,N,O,P type
```

## 5. DG-TR-003. Жизненный цикл требования

```mermaid
flowchart TD
    A[Источник требования] --> B[Формулировка]
    B --> C[Категория]
    C --> D[Причина]
    D --> E[Критерий выполнения]
    E --> F[Способ проверки]
    F --> G[Влияние на следующие этапы]
    G --> H[Статус]
    H --> I[Передача в анкету]
    I --> J[Передача в критерии выбора инструментария]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J type
```

## 6. DG-TR-004. Проверяемое требование

```mermaid
flowchart TD
    A[Техническое требование] --> B[Система должна]
    A --> C[Источник]
    A --> D[Критерий выполнения]
    A --> E[Способ проверки]
    A --> F[Влияние]
    A --> G[Статус]

    B --> B1[Обязанность системы]
    C --> C1[Откуда появилось]
    D --> D1[Как понять что выполнено]
    E --> E1[Как подтвердить]
    F --> F1[На что влияет дальше]
    G --> G1[Draft Approved Changed Deprecated]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,B1,C1,D1,E1,F1,G1 type
```

## 7. DG-TR-005. Требования не выбирают инструменты

```mermaid
flowchart TD
    A[Потребность системы] --> B[Техническое требование]
    B --> C[Критерий выполнения]
    C --> D[Способ проверки]
    D --> E[Критерий выбора инструмента]
    E --> F[Выбор инструментария]

    B --> G[Запрещено: выбрать инструмент сразу]
    G --> H[Пример ошибки: использовать SQLite]
    C --> I[Правильно: данные должны сохраняться между запусками]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I type
```

## 8. DG-TR-006. Влияние требований на следующие этапы

```mermaid
flowchart TD
    A[Технические требования] --> B[Выбор инструментария]
    A --> C[Архитектура реализации]
    A --> D[Тестирование]
    A --> E[Эксплуатация]
    A --> F[Сопровождение]

    B --> B1[Критерии выбора]
    C --> C1[Структура реализации]
    D --> D1[Тестовые сценарии]
    E --> E1[Рабочие инструкции]
    F --> F1[Диагностика и обновления]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,B1,C1,D1,E1,F1 type
```

## 9. DG-TR-007. Выход в карту требований и инструментария

```mermaid
flowchart TD
    A[Утверждённое требование] --> B[Требование влияет на инструмент]
    B --> C{Влияет?}
    C -->|Нет| D[Передать в тестирование или реализацию]
    C -->|Да| E[Requirements To Toolchain Map]
    E --> F[Критерий выбора]
    F --> G[Roadmap Toolchain Selection]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,D,E,F,G type
```

## 10. DG-TR-008. Открытые вопросы требований

```mermaid
flowchart TD
    A[Неизвестный параметр] --> B[Открытый вопрос]
    B --> C[Почему важен]
    B --> D[Какой этап блокирует]
    B --> E[Кто может дать ответ]
    B --> F[Что нельзя делать до ответа]
    F --> G[Запрет на догадки]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G type
```

## 11. Следующий шаг

После просмотра диаграмм необходимо вернуться к связанному roadmap-документу или карте, где эти схемы применяются.

## 12. История изменений

- Initial version: созданы диаграммы этапа технических требований.
- Updated: документ приведён к единому визуальному формату проекта.
