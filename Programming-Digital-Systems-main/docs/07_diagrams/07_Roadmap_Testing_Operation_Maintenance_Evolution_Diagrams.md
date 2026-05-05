# Roadmap Testing Operation Maintenance Evolution Diagrams / Диаграммы тестирования, эксплуатации, сопровождения и развития

## 1. Назначение документа

`07_07_Roadmap_Testing_Operation_Maintenance_Evolution_Diagrams.md` хранит диаграммы жизненного цикла системы после архитектуры реализации и кода.

Документ визуализирует тестирование, эксплуатацию, сопровождение, развитие системы и возвраты к предыдущим этапам.

Документ не заменяет roadmap-документы и анкеты этих этапов.

> [!info] Главное
> Документ хранит визуальные схемы, которые помогают читать структуру, связи и маршрут.

## 2. Связанные документы

- [[docs/03_roadmaps/07_Roadmap_Testing|Roadmap: Testing]]
- [[docs/04_questionnaires/07_Questionnaire_Testing|Questionnaire: Testing]]
- [[docs/03_roadmaps/08_Roadmap_Operation|Roadmap: Operation]]
- [[docs/04_questionnaires/08_Questionnaire_Operation|Questionnaire: Operation]]
- [[docs/03_roadmaps/09_Roadmap_Maintenance|Roadmap: Maintenance]]
- [[docs/04_questionnaires/09_Questionnaire_Maintenance|Questionnaire: Maintenance]]
- [[docs/03_roadmaps/10_Roadmap_System_Evolution|Roadmap: System Evolution]]
- [[docs/04_questionnaires/10_Questionnaire_System_Evolution|Questionnaire: System Evolution]]
- [[docs/07_diagrams/06_Roadmap_Implementation_Architecture_Diagrams|Roadmap Implementation Architecture Diagrams]]
- [[docs/07_diagrams/00_Development_Route_Diagrams|Development Route Diagrams]]

## 3. DG-LIFE-001. Переход от реализации к жизненному циклу

```mermaid
flowchart TD
    A[Архитектура реализации] --> B[Код]
    B --> C[Тестирование]
    C --> D{Готово к эксплуатации?}
    D -->|Нет| E[Исправление]
    E --> C
    D -->|Да| F[Эксплуатация]
    F --> G[Сопровождение]
    G --> H[Развитие системы]
    H --> C

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,E,F,G,H type
```

## 4. DG-LIFE-002. Карта тестирования

```mermaid
flowchart TD
    A[Тестирование] --> B[Проверка требований]
    A --> C[Unit тесты]
    A --> D[Integration тесты]
    A --> E[System тесты]
    A --> F[Acceptance тесты]
    A --> G[Тестирование данных]
    A --> H[Тестирование ошибок]
    A --> I[Тестирование интерфейсов]
    A --> J[Производительность]
    A --> K[Безопасность]
    A --> L[Регрессия]
    A --> M[Ручная проверка]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L,M type
```

## 5. DG-LIFE-003. Жизненный цикл теста

```mermaid
flowchart TD
    A[Источник теста] --> B[Тестовый сценарий]
    B --> C[Тестовые данные]
    C --> D[Выполнение]
    D --> E[Фактический результат]
    E --> F{Ожидаемый результат получен?}
    F -->|Да| G[Passed]
    F -->|Нет| H[Failed]
    H --> I[Анализ причины]
    I --> J{Где ошибка?}
    J -->|Код| K[Исправление реализации]
    J -->|Тест| L[Исправление теста]
    J -->|Требование| M[Возврат к требованиям]
    J -->|Архитектура| N[Возврат к архитектуре]
    K --> D
    L --> D

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,G,H,I,K,L,M,N type
```

## 6. DG-LIFE-004. Карта эксплуатации

```mermaid
flowchart TD
    A[Готовая система] --> B[Запуск]
    B --> C[Рабочий сценарий]
    C --> D[Входные данные]
    D --> E[Обработка]
    E --> F[Результат]
    E --> G[Эксплуатационная ошибка]
    G --> H[Сообщение пользователю]
    G --> I[Лог]
    I --> J[Сопровождение]
    F --> K[Остановка или повторный запуск]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K type
```

## 7. DG-LIFE-005. Эксплуатационные данные для сопровождения

```mermaid
flowchart TD
    A[Эксплуатация] --> B[Ошибки пользователя]
    A --> C[Логи]
    A --> D[Жалобы]
    A --> E[Неясные сценарии]
    A --> F[Повторяющиеся проблемы]
    A --> G[Предложения улучшений]

    B --> H[Сопровождение]
    C --> H
    D --> H
    E --> H
    F --> H
    G --> I[Развитие системы]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I type
```

## 8. DG-LIFE-006. Карта сопровождения

```mermaid
flowchart TD
    A[Инцидент или дефект] --> B[Регистрация]
    B --> C[Воспроизведение]
    C --> D[Анализ причины]
    D --> E[План исправления]
    E --> F[Исправление]
    F --> G[Целевая проверка]
    G --> H[Регрессия]
    H --> I{Проверка пройдена?}
    I -->|Нет| D
    I -->|Да| J[Обновление документации]
    J --> K[Выпуск обновления]
    K --> L[Эксплуатация]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,J,K,L type
```

## 9. DG-LIFE-007. Разделение сопровождения и развития

```mermaid
flowchart TD
    A[Изменение после эксплуатации] --> B{Тип изменения}
    B -->|Исправляет дефект| C[Сопровождение]
    B -->|Добавляет новую возможность| D[Развитие системы]
    B -->|Меняет требования| E[Возврат к требованиям]
    B -->|Меняет архитектуру| F[Возврат к архитектуре]
    B -->|Меняет инструмент| G[Возврат к выбору инструментария]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class C,D,E,F,G type
```

## 10. DG-LIFE-008. Карта развития системы

```mermaid
flowchart TD
    A[Запрос развития] --> B[Классификация запроса]
    B --> C[Анализ влияния]
    C --> D[Влияние на проектирование системы]
    C --> E[Влияние на требования]
    C --> F[Влияние на архитектуру]
    C --> G[Влияние на инструментарий]
    C --> H[Влияние на реализацию]
    C --> I[Влияние на тестирование]
    C --> J[Влияние на эксплуатацию]
    J --> K[Проверка совместимости]
    K --> L[Решение]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J,K,L type
```

## 11. DG-LIFE-009. Обратная совместимость и миграция

```mermaid
flowchart TD
    A[Изменение системы] --> B{Ломает существующее?}
    B -->|Нет| C[Совместимое развитие]
    B -->|Да| D[Нужна миграция или breaking change]
    D --> E[Данные]
    D --> F[Сценарии]
    D --> G[Интерфейсы]
    D --> H[Отчёты]
    D --> I[Интеграции]
    E --> J[План миграции]
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
    class C,D,E,F,G,H,I,J type
```

## 12. DG-LIFE-010. Возврат из развития к нужному этапу

```mermaid
flowchart TD
    A[Анализ развития] --> B{Что меняется?}
    B -->|Сущности данные правила| C[Проектирование системы]
    B -->|Слои модули интерфейсы| D[Архитектура системы]
    B -->|Проверяемые условия| E[Технические требования]
    B -->|Инструменты| F[Выбор инструментария]
    B -->|Структура проекта| G[Архитектура реализации]
    B -->|Проверки| H[Тестирование]
    B -->|Рабочие сценарии| I[Эксплуатация]

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class C,D,E,F,G,H,I type
```

## 13. DG-LIFE-011. Полный цикл после выпуска

```mermaid
flowchart TD
    A[Выпуск версии] --> B[Эксплуатация]
    B --> C[Наблюдение]
    C --> D[Инциденты]
    C --> E[Идеи улучшения]
    D --> F[Сопровождение]
    E --> G[Развитие]
    F --> H[Patch update]
    G --> I[Feature update]
    H --> J[Тестирование]
    I --> J
    J --> A

    classDef root fill:#dbeafe,stroke:#2563eb,stroke-width:2px
    classDef type fill:#e0f2fe,stroke:#0284c7,stroke-width:1px
    classDef step fill:#f8fafc,stroke:#64748b,stroke-width:1px
    classDef success fill:#dcfce7,stroke:#16a34a,stroke-width:2px
    classDef warning fill:#fee2e2,stroke:#dc2626,stroke-width:1px

    class A root
    class B,C,D,E,F,G,H,I,J type
```

## 14. Следующий шаг

После просмотра диаграмм необходимо вернуться к связанному roadmap-документу или карте, где эти схемы применяются.

## 15. История изменений

- Initial version: созданы диаграммы тестирования, эксплуатации, сопровождения, развития и возвратов по жизненному циклу системы.
- Updated: документ приведён к единому визуальному формату проекта.
