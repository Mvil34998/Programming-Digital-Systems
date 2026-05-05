# Roadmap System Architecture Diagrams / Диаграммы архитектуры системы

## 1. Назначение документа

`02_Roadmap_System_Architecture_Diagrams.md` хранит диаграммы этапа проектирования архитектуры системы.

Документ визуализирует, как результаты проектирования системы превращаются в слои, модули, модели, интерфейсы, зависимости, конфигурации и точки расширения.

Документ не заменяет [[docs/03_roadmaps/02_Roadmap_System_Architecture_Design|Roadmap: System Architecture Design]] и [[docs/04_questionnaires/02_Questionnaire_System_Architecture_Design|Questionnaire: System Architecture Design]].

> [!info] Главное
> Документ хранит визуальные схемы, которые помогают читать структуру, связи и маршрут.

## 2. Связанные документы

- [[docs/03_roadmaps/02_Roadmap_System_Architecture_Design|Roadmap: System Architecture Design]]
- [[docs/04_questionnaires/02_Questionnaire_System_Architecture_Design|Questionnaire: System Architecture Design]]
- [[docs/03_roadmaps/01_Roadmap_System_Design|Roadmap: System Design]]
- [[docs/04_questionnaires/01_Questionnaire_System_Design|Questionnaire: System Design]]
- [[docs/05_encyclopedia/Architecture|Architecture]]
- [[docs/05_encyclopedia/Interfaces|Interfaces]]
- [[docs/07_diagrams/01_Roadmap_System_Design_Diagrams|Roadmap System Design Diagrams]]

## 3. DG-ARCH-001. Вход в архитектуру системы

```mermaid
flowchart TD
    A[Проектирование системы] --> B[Сущности]
    A --> C[Данные]
    A --> D[Правила]
    A --> E[Состояния]
    A --> F[События]
    A --> G[Потоки]
    A --> H[Хранение]
    A --> I[Ошибки]

    B --> J[Архитектура системы]
    C --> J
    D --> J
    E --> J
    F --> J
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

## 4. DG-ARCH-002. Основные элементы архитектуры системы

```mermaid
flowchart TD
    A[Архитектура системы] --> B[Слои]
    A --> C[Модули]
    A --> D[Модели]
    A --> E[Интерфейсы]
    A --> F[Зависимости]
    A --> G[Конфигурации]
    A --> H[Точки расширения]
    A --> I[Архитектурные ограничения]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I type
```

## 5. DG-ARCH-003. Слои архитектуры

```mermaid
flowchart TD
    A[Слои системы] --> B[Слой представления]
    A --> C[Слой сценариев]
    A --> D[Слой бизнес логики]
    A --> E[Слой доменной модели]
    A --> F[Слой данных]
    A --> G[Слой хранения]
    A --> H[Слой инфраструктуры]
    A --> I[Слой конфигурации]
    A --> J[Слой ошибок и логирования]

    B --> K[Пользовательское взаимодействие]
    C --> L[Координация сценариев]
    D --> M[Правила и решения]
    E --> N[Смысловые модели]
    F --> O[Структуры данных]
    G --> P[Сохранение и чтение]
    H --> Q[Файлы сеть оборудование ОС]
    I --> R[Настройки]
    J --> S[Диагностика]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S type
```

## 6. DG-ARCH-004. Модули внутри слоёв

```mermaid
flowchart TD
    A[Слой] --> B[Модуль]
    B --> C[Назначение]
    B --> D[Вход]
    B --> E[Выход]
    B --> F[Зависимости]
    B --> G[Ошибки]
    B --> H[Тестируемость]

    C --> I[Одна основная ответственность]
    F --> J[Явные допустимые зависимости]
    H --> K[Проверяемое поведение]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K type
```

## 7. DG-ARCH-005. Модели архитектуры

```mermaid
flowchart TD
    A[Модели] --> B[Доменные модели]
    A --> C[Модели данных]
    A --> D[Модели входа]
    A --> E[Модели выхода]
    A --> F[Модели конфигурации]
    A --> G[Модели состояния]
    A --> H[Модели событий]
    A --> I[Модели ошибок]
    A --> J[Модели хранения]
    A --> K[Модели интерфейсов]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K type
```

## 8. DG-ARCH-006. Интерфейсы и границы взаимодействия

```mermaid
flowchart TD
    A[Интерфейс] --> B[Участник 1]
    A --> C[Участник 2]
    A --> D[Входные данные]
    A --> E[Выходные данные]
    A --> F[Допустимые действия]
    A --> G[Ошибки интерфейса]
    A --> H[Ограничения]

    B --> I[Пользователь модуль система устройство]
    C --> I

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I type
```

## 9. DG-ARCH-007. Направление зависимостей

```mermaid
flowchart TD
    A[Представление] --> B[Сценарии приложения]
    B --> C[Бизнес логика]
    C --> D[Доменная модель]
    B --> E[Интерфейсы адаптеров]
    F[Инфраструктура] --> E
    G[Хранение] --> E
    H[Внешние системы] --> E

    D --> I[Не зависит от инфраструктуры]
    C --> I

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I type
```

## 10. DG-ARCH-008. Конфигурации и точки расширения

```mermaid
flowchart TD
    A[Архитектура системы] --> B[Конфигурации]
    A --> C[Точки расширения]

    B --> B1[Параметры без изменения кода]
    B --> B2[Правила проверки]
    B --> B3[Ошибки конфигурации]

    C --> C1[Новые данные]
    C --> C2[Новые правила]
    C --> C3[Новые форматы]
    C --> C4[Новые интеграции]
    C --> C5[Новые интерфейсы]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,B1,B2,B3,C1,C2,C3,C4,C5 type
```

## 11. DG-ARCH-009. Выход в технические требования

```mermaid
flowchart TD
    A[Архитектура системы завершена] --> B[Слои]
    A --> C[Модули]
    A --> D[Модели]
    A --> E[Интерфейсы]
    A --> F[Зависимости]
    A --> G[Конфигурации]
    A --> H[Точки расширения]
    A --> I[Архитектурные ограничения]

    B --> J[Технические требования]
    C --> J
    D --> J
    E --> J
    F --> J
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

## 12. Следующий шаг

После просмотра диаграмм необходимо вернуться к связанному roadmap-документу или карте, где эти схемы применяются.

## 13. История изменений

- Initial version: созданы диаграммы этапа проектирования архитектуры системы.
- Updated: документ приведён к единому визуальному формату проекта.
