# Проверка метамодели: Python File Processing Utility

## 1. Назначение документа

`01_Python_File_Processing_Utility_Metamodel_Check.md` проверяет рабочую форму метамодели Digital System CAD на первом примере:

- [[docs/06_examples/Scripts/Python_File_Processing_Utility|Python File Processing Utility]]
- [[docs/04_questionnaires/01_Questionnaire_System_Design_Filled_Python_File_Processing_Utility|Filled Questionnaire: Python File Processing Utility]]

Документ не создаёт финальный SDD и не закрывает открытые вопросы. Он проверяет, можно ли из существующих материалов получить:

- элементы модели;
- типы связей;
- структурированные факты;
- реестры;
- трассировку;
- область будущего SDD;
- разрывы и неполноту модели.

> [!info] Главное
> Первый пример подтверждает, что даже простая Python-утилита раскладывается на элементы, связи, факты, реестры и SDD-представления. Но пример также показывает, что без уточнения открытых вопросов нельзя формировать полный технический SDD.

## 2. Входные источники

| Source ID     | Источник                                                                                        | Роль                             |                                  |
| ------------- | ----------------------------------------------------------------------------------------------- | -------------------------------- | -------------------------------- |
| SRC-PY-EX-001 | [[docs/06_examples/Scripts/Python_File_Processing_Utility]]                                     | Python File Processing Utility]] | учебное описание системы         |
| SRC-PY-Q-001  | [[docs/04_questionnaires/01_Questionnaire_System_Design_Filled_Python_File_Processing_Utility]] | Filled Questionnaire]]           | структурированные факты анкеты   |
| SRC-MM-001    | [[docs/08_digital_system_cad/metamodel/01_Model_Elements]]                                      | Model Elements]]                 | типы элементов                   |
| SRC-MM-002    | [[docs/08_digital_system_cad/metamodel/02_Model_Relations]]                                     | Model Relations]]                | типы связей                      |
| SRC-MM-003    | [[docs/08_digital_system_cad/metamodel/03_Structured_Facts]]                                    | Structured Facts]]               | форма факта                      |
| SRC-MM-004    | [[docs/08_digital_system_cad/metamodel/04_Model_Registers]]                                     | Model Registers]]                | реестры как представления        |
| SRC-MM-005    | [[docs/08_digital_system_cad/metamodel/06_Traceability]]                                        | Traceability]]                   | правила трассировки              |
| SRC-MM-006    | [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model]]                                      | SDD From Model]]                 | правила отображения модели в SDD |

## 3. Проверяемая система

```yaml
id: PRJ-PYFILE-001
type: Project
name: Python File Processing Utility
definition: "Локальная Python CLI-утилита, которая читает .txt файлы из входной папки, считает строки и слова, записывает CSV-отчёт и лог обработки."
purpose: "Дать пользователю статистику по файлам без изменения исходных файлов."
source:
  - SRC-PY-EX-001
  - SRC-PY-Q-001
status: candidate
context: "Скрипты / утилита автоматизации"
open_questions:
  - OQ-PY-DATA-001
  - OQ-PY-RULE-001
  - OQ-PY-STOR-001
  - OQ-PY-ERR-001
```

## 4. Извлечённые элементы модели

### 4.1. Реестр требований

| ID         | Название                           | Определение                                                                    | Источник      | Проверка    | Статус    | Разрывы                        |
| ---------- | ---------------------------------- | ------------------------------------------------------------------------------ | ------------- | ----------- | --------- | ------------------------------ |
| REQ-PY-001 | Проверка входной папки             | Система должна проверять существование входной папки до начала обработки.      | SRC-PY-EX-001 | TEST-PY-001 | candidate | нет                            |
| REQ-PY-002 | Обработка только `.txt` файлов     | Система должна обрабатывать только `.txt` файлы и игнорировать другие форматы. | SRC-PY-EX-001 | TEST-PY-002 | candidate | нет                            |
| REQ-PY-003 | Подсчёт строк и слов               | Система должна считать строки и слова для каждого успешно прочитанного файла.  | SRC-PY-EX-001 | TEST-PY-003 | candidate | OQ-PY-RULE-001                 |
| REQ-PY-004 | Сохранение CSV-отчёта              | Система должна сохранять CSV-отчёт со статистикой файлов.                      | SRC-PY-EX-001 | TEST-PY-004 | candidate | OQ-PY-DATA-001, OQ-PY-STOR-001 |
| REQ-PY-005 | Логирование ошибок обработки       | Система должна записывать ошибки обработки в лог.                              | SRC-PY-EX-001 | TEST-PY-005 | candidate | нет                            |
| REQ-PY-006 | Сохранность исходных файлов        | Система не должна изменять исходные файлы.                                     | SRC-PY-Q-001  | TEST-PY-006 | candidate | нет                            |
| REQ-PY-007 | Поведение при пустой входной папке | Система должна определить поведение, если во входной папке нет `.txt` файлов.  | SRC-PY-Q-001  | TEST-PY-007 | draft     | OQ-PY-ERR-001                  |

### 4.2. Реестр акторов

| ID | Название | Тип | Определение | Интерфейсы | Статус | Разрывы |
|---|---|---|---|---|---|---|
| ACT-PY-001 | Пользователь | человек | Пользователь, который запускает утилиту и читает отчёт или лог. | INT-PY-001 | candidate | нет |
| ACT-PY-002 | Файловая система | внешняя система | Локальная файловая система, которая хранит входные файлы, отчёт и лог. | INT-PY-002 | candidate | нет |

### 4.3. Реестр сущностей

| ID | Название | Тип | Определение | Поля данных | Статус | Разрывы |
|---|---|---|---|---|---|---|
| ENT-PY-001 | InputFolder | информационная сущность | Папка, содержащая файлы для обработки. | DATA-PY-001 | candidate | нет |
| ENT-PY-002 | TextFile | предметная сущность | `.txt` файл, который обрабатывает утилита. | DATA-PY-002, DATA-PY-003 | candidate | нет |
| ENT-PY-003 | FileStats | информационная сущность | Статистика по одному обработанному файлу. | DATA-PY-004, DATA-PY-005, DATA-PY-006, DATA-PY-007, DATA-PY-008 | candidate | OQ-PY-DATA-001 |
| ENT-PY-004 | ProcessingResult | информационная сущность | Итог обработки набора файлов. | DATA-PY-009 | candidate | частично |
| ENT-PY-005 | CsvReport | результирующая сущность | CSV-отчёт, который формируется для пользователя. | DATA-PY-010 | candidate | OQ-PY-DATA-001, OQ-PY-STOR-001 |
| ENT-PY-006 | ProcessingLog | результирующая сущность | Файл лога с диагностической информацией и ошибками. | DATA-PY-011 | candidate | нет |

### 4.4. Реестр полей данных

| ID          | Название              | Владелец                | Тип / формат      | Обязательность | Проверяется правилом | Разрывы                                 |
| ----------- | --------------------- | ----------------------- | ----------------- | -------------- | -------------------- | --------------------------------------- |
| DATA-PY-001 | input_folder_path     | ENT-PY-001 / INT-PY-001 | путь              | да             | RULE-PY-001          | нет                                     |
| DATA-PY-002 | file_name             | ENT-PY-002 / ENT-PY-003 | строка            | да             | RULE-PY-002          | нет                                     |
| DATA-PY-003 | text_file_content     | ENT-PY-002              | текст             | да             | RULE-PY-003          | кодировка не определена                 |
| DATA-PY-004 | line_count            | ENT-PY-003              | integer           | да             | RULE-PY-004          | нет                                     |
| DATA-PY-005 | word_count            | ENT-PY-003              | integer           | да             | RULE-PY-005          | OQ-PY-RULE-001                          |
| DATA-PY-006 | status                | ENT-PY-003              | enum              | да             | RULE-PY-006          | допустимые значения определены частично |
| DATA-PY-007 | error_message         | ENT-PY-003              | строка / nullable | условно        | RULE-PY-007          | нет                                     |
| DATA-PY-008 | file_path             | ENT-PY-003              | путь              | опционально    | RULE-PY-008          | понадобится при рекурсивной обработке   |
| DATA-PY-009 | processed_files_count | ENT-PY-004              | integer           | опционально    | RULE-PY-009          | нет в текущих требованиях               |
| DATA-PY-010 | report_csv_columns    | ENT-PY-005              | CSV-схема         | да             | RULE-PY-010          | OQ-PY-DATA-001                          |
| DATA-PY-011 | log_message           | ENT-PY-006              | текст             | да             | RULE-PY-011          | нет                                     |

### 4.5. Реестр правил

| ID          | Название                               | Условие                                                         | Цель        | Поведение при нарушении                | Ошибка     | Тест        | Разрывы                                 |
| ----------- | -------------------------------------- | --------------------------------------------------------------- | ----------- | -------------------------------------- | ---------- | ----------- | --------------------------------------- |
| RULE-PY-001 | Входная папка должна существовать      | до обработки путь входной папки указывает на существующую папку | DATA-PY-001 | остановить обработку и показать ошибку | ERR-PY-001 | TEST-PY-001 | нет                                     |
| RULE-PY-002 | Обрабатываются только `.txt` файлы     | найденный файл имеет расширение `.txt`                          | ENT-PY-002  | игнорировать остальные файлы           | ERR-PY-002 | TEST-PY-002 | нет                                     |
| RULE-PY-003 | Файл должен быть читаемым              | файл можно прочитать как текст                                  | DATA-PY-003 | записать ошибку в лог и продолжить     | ERR-PY-003 | TEST-PY-005 | политика кодировок определена частично  |
| RULE-PY-004 | Подсчёт строк                          | содержимое файла разбивается на строки                          | DATA-PY-004 | тест падает, если количество неверное  | ERR-PY-004 | TEST-PY-003 | нет                                     |
| RULE-PY-005 | Подсчёт слов                           | содержимое файла разбивается на слова                           | DATA-PY-005 | тест падает, если количество неверное  | ERR-PY-005 | TEST-PY-003 | OQ-PY-RULE-001                          |
| RULE-PY-006 | Статус строки отчёта                   | каждый результат файла имеет статус обработки                   | DATA-PY-006 | некорректная строка отчёта             | ERR-PY-006 | TEST-PY-004 | допустимые значения определены частично |
| RULE-PY-007 | Сообщение ошибки для неуспешного файла | результат неуспешного файла содержит сообщение ошибки           | DATA-PY-007 | некорректная диагностика               | ERR-PY-007 | TEST-PY-005 | нет                                     |
| RULE-PY-008 | Исходные файлы только читаются         | утилита не пишет во входные файлы                               | ENT-PY-002  | нарушение ограничения проекта          | ERR-PY-008 | TEST-PY-006 | нет                                     |
| RULE-PY-009 | Поведение при пустой папке             | не найдено `.txt` файлов                                        | ENT-PY-001  | требуется решение                      | ERR-PY-009 | TEST-PY-007 | OQ-PY-ERR-001                           |
| RULE-PY-010 | Схема CSV-отчёта                       | колонки отчёта соответствуют обязательной схеме                 | ENT-PY-005  | некорректный отчёт                     | ERR-PY-010 | TEST-PY-004 | OQ-PY-DATA-001                          |
| RULE-PY-011 | Лог фиксирует ошибки обработки         | возникает ошибка обработки                                      | ENT-PY-006  | отсутствует диагностика                | ERR-PY-011 | TEST-PY-005 | нет                                     |

### 4.6. Реестр ошибок

| ID | Название | Причина | Критичность | Реакция | Тест | Разрывы |
|---|---|---|---|---|---|---|
| ERR-PY-001 | Входная папка отсутствует | входная папка не существует | fatal | остановить обработку и сообщить пользователю | TEST-PY-001 | нет |
| ERR-PY-002 | Файл не `.txt` проигнорирован | расширение файла не `.txt` | info | игнорировать файл | TEST-PY-002 | нет |
| ERR-PY-003 | Файл не удалось прочитать | файл нельзя прочитать | recoverable | записать ошибку в лог и продолжить | TEST-PY-005 | нет |
| ERR-PY-004 | Неверный подсчёт строк | расчёт не совпадает с ожидаемым количеством строк | error | провалить тест / исправить расчёт | TEST-PY-003 | нет |
| ERR-PY-005 | Неверный подсчёт слов | правило расчёта слов неясно или неверно | error | провалить тест / определить правило | TEST-PY-003 | OQ-PY-RULE-001 |
| ERR-PY-006 | Некорректный статус в отчёте | статус строки отсутствует или недопустим | error | провалить проверку отчёта | TEST-PY-004 | частично |
| ERR-PY-007 | Нет сообщения об ошибке | неуспешный файл не имеет диагностического сообщения | warning | провалить диагностический тест | TEST-PY-005 | нет |
| ERR-PY-008 | Исходный файл изменён | утилита меняет входной файл | blocker | провалить приёмку | TEST-PY-006 | нет |
| ERR-PY-009 | Поведение при пустой папке не определено | не найдено `.txt` файлов | warning | требуется решение | TEST-PY-007 | OQ-PY-ERR-001 |
| ERR-PY-010 | Не удалось записать отчёт | CSV нельзя записать | fatal | сообщить пользователю и завершить запуск ошибкой | TEST-PY-008 | теста нет в исходном примере |
| ERR-PY-011 | Не удалось записать лог | лог нельзя создать или записать | warning/error | диагностика ухудшается или запуск завершается ошибкой | TEST-PY-009 | критичность неясна |

### 4.7. Реестр событий

| ID | Название | Источник | Запускает | Данные | Разрывы |
|---|---|---|---|---|---|
| EVENT-PY-001 | start_requested | Пользователь | FLOW-PY-001 | DATA-PY-001 | нет |
| EVENT-PY-002 | input_folder_checked | SVC-PY-001 ProcessingUseCase | FLOW-PY-002 | DATA-PY-001 | нет |
| EVENT-PY-003 | file_found | SVC-PY-002 FileDiscoveryService | FLOW-PY-003 | DATA-PY-002 | нет |
| EVENT-PY-004 | file_read_success | SVC-PY-003 TextFileReader | FLOW-PY-004 | DATA-PY-003 | нет |
| EVENT-PY-005 | file_read_failed | SVC-PY-003 TextFileReader | FLOW-PY-006 | ERR-PY-003 | нет |
| EVENT-PY-006 | file_stats_created | SVC-PY-004 StatisticsService | FLOW-PY-005 | ENT-PY-003 | нет |
| EVENT-PY-007 | report_write_requested | SVC-PY-001 ProcessingUseCase | FLOW-PY-007 | ENT-PY-004 | нет |
| EVENT-PY-008 | report_written | SVC-PY-005 CsvReportService | completed state | ENT-PY-005 | нет |

### 4.8. Реестр потоков

| ID | Название | Источник | Получатель | Передаваемый объект | Триггер | Ошибки |
|---|---|---|---|---|---|---|
| FLOW-PY-001 | Запуск обработки | ACT-PY-001 | SVC-PY-001 | DATA-PY-001 | EVENT-PY-001 | ERR-PY-001 |
| FLOW-PY-002 | Поиск файлов | SVC-PY-001 | SVC-PY-002 | DATA-PY-001 | EVENT-PY-002 | ERR-PY-009 |
| FLOW-PY-003 | Чтение текстового файла | SVC-PY-002 | SVC-PY-003 | ENT-PY-002 | EVENT-PY-003 | ERR-PY-003 |
| FLOW-PY-004 | Подсчёт статистики | SVC-PY-003 | SVC-PY-004 | DATA-PY-003 | EVENT-PY-004 | ERR-PY-004, ERR-PY-005 |
| FLOW-PY-005 | Сбор FileStats | SVC-PY-004 | SVC-PY-001 | ENT-PY-003 | EVENT-PY-006 | нет |
| FLOW-PY-006 | Логирование ошибки чтения | SVC-PY-003 | SVC-PY-006 | ERR-PY-003 | EVENT-PY-005 | ERR-PY-011 |
| FLOW-PY-007 | Запись CSV-отчёта | SVC-PY-001 | SVC-PY-005 | ENT-PY-004 | EVENT-PY-007 | ERR-PY-010 |
| FLOW-PY-008 | Запись лога обработки | SVC-PY-006 | STOR-PY-002 | ENT-PY-006 | события обработки | ERR-PY-011 |

### 4.9. Реестр хранения

| ID | Название | Хранимые элементы | Назначение | Жизненный цикл | Разрывы |
|---|---|---|---|---|---|
| STOR-PY-001 | CSV report file | ENT-PY-005, ENT-PY-003 | результат для пользователя | создаётся после обработки | OQ-PY-STOR-001 |
| STOR-PY-002 | Processing log file | ENT-PY-006, ERR-PY-* | диагностика | создаётся во время обработки | критичность ошибки записи лога неясна |
| STOR-PY-003 | Input files | ENT-PY-002 | исходные данные | входные данные только для чтения | нет |

### 4.10. Реестр интерфейсов

| ID | Название | Вид | Участники | Вход | Выход | Ошибки | Разрывы |
|---|---|---|---|---|---|---|---|
| INT-PY-001 | CLI parameters | CLI | ACT-PY-001, PRJ-PYFILE-001 | DATA-PY-001, output path | результат запуска / сообщения | ERR-PY-001 | output path недоописан |
| INT-PY-002 | File system access | файловая система | PRJ-PYFILE-001, ACT-PY-002 | пути файлов | содержимое файла, результат записи | ERR-PY-003, ERR-PY-010, ERR-PY-011 | нет |
| INT-PY-003 | CSV report output | файловый вывод | PRJ-PYFILE-001, ACT-PY-001 | ENT-PY-003 | ENT-PY-005 | ERR-PY-010 | OQ-PY-DATA-001 |
| INT-PY-004 | Processing log output | файловый вывод | PRJ-PYFILE-001, ACT-PY-001 | ERR-PY-* | ENT-PY-006 | ERR-PY-011 | нет |

### 4.11. Реестр модулей

После уточнения правила атомизации имена `FileDiscoveryService`, `TextFileReader`, `StatisticsService`, `CsvReportService`, `LoggingService` не должны быть Module по умолчанию. Это исполнители поведения, поэтому они выделяются как `Service`, а Module остаётся областью ответственности.

| ID | Название | Слой | Ответственность | Содержит Service | Предоставляет / использует | Разрывы |
|---|---|---|---|---|---|---|
| MOD-PY-001 | ProcessingModule | Application Layer | координация сценария обработки | SVC-PY-001 | использует MOD-PY-002..005 | нет |
| MOD-PY-002 | ScanningModule | Infrastructure Layer | поиск и чтение исходных файлов | SVC-PY-002, SVC-PY-003 | использует INT-PY-002 | политика кодировок частичная |
| MOD-PY-003 | StatisticsModule | Domain Layer | расчёт статистики по тексту | SVC-PY-004 | использует ENT-PY-003 | OQ-PY-RULE-001 |
| MOD-PY-004 | ReportingModule | Infrastructure Layer | формирование и запись CSV-отчёта | SVC-PY-005 | предоставляет INT-PY-003 | OQ-PY-DATA-001 |
| MOD-PY-005 | LoggingModule | Infrastructure Layer | запись журнала обработки | SVC-PY-006 | предоставляет INT-PY-004 | критичность ERR-PY-011 неясна |

### 4.11.1. Реестр сервисов

| ID | Название | Module | Операция | Обрабатывает / создаёт | Реализуется | Разрывы |
|---|---|---|---|---|---|---|
| SVC-PY-001 | ProcessingUseCase | MOD-PY-001 | координирует основной сценарий | читает InputFolder, запускает сервисы | CODE-PY-001 | нет |
| SVC-PY-002 | FileDiscoveryService | MOD-PY-002 | находит `.txt` файлы | читает ENT-PY-001, создаёт список SourceFile | CODE-PY-002 | нет |
| SVC-PY-003 | TextFileReader | MOD-PY-002 | читает содержимое файла | читает ENT-PY-002, создаёт ENT-PY-003 | CODE-PY-002 | политика кодировок частичная |
| SVC-PY-004 | StatisticsService | MOD-PY-003 | считает строки и слова | обрабатывает ENT-PY-003, создаёт ENT-PY-004 | CODE-PY-003 | OQ-PY-RULE-001 |
| SVC-PY-005 | CsvReportService | MOD-PY-004 | записывает CSV-отчёт | читает ENT-PY-004, создаёт ENT-PY-005 | CODE-PY-004 | OQ-PY-DATA-001 |
| SVC-PY-006 | LoggingService | MOD-PY-005 | записывает лог обработки | создаёт ENT-PY-006 | CODE-PY-005 | критичность ERR-PY-011 неясна |

### 4.12. Реестр тестовых случаев

| ID          | Название                          | Проверяет                            | Ожидаемый результат                           | Разрывы                |
| ----------- | --------------------------------- | ------------------------------------ | --------------------------------------------- | ---------------------- |
| TEST-PY-001 | Тест отсутствующей входной папки  | REQ-PY-001, ERR-PY-001               | обработка останавливается с понятной ошибкой  | нет                    |
| TEST-PY-002 | Тест фильтра `.txt`               | REQ-PY-002, RULE-PY-002              | выбраны только `.txt` файлы                   | нет                    |
| TEST-PY-003 | Тест подсчёта статистики          | REQ-PY-003, RULE-PY-004, RULE-PY-005 | строки и слова совпадают с ожидаемыми         | OQ-PY-RULE-001         |
| TEST-PY-004 | Тест CSV-отчёта                   | REQ-PY-004, RULE-PY-010              | отчёт содержит обязательные колонки и строки  | OQ-PY-DATA-001         |
| TEST-PY-005 | Тест логирования ошибки чтения    | REQ-PY-005, ERR-PY-003               | ошибка записана в лог, обработка продолжается | нет                    |
| TEST-PY-006 | Тест неизменности исходных файлов | REQ-PY-006, RULE-PY-008              | содержимое входных файлов не изменилось       | нет                    |
| TEST-PY-007 | Тест поведения пустой папки       | REQ-PY-007, ERR-PY-009               | поведение соответствует принятому решению     | OQ-PY-ERR-001          |
| TEST-PY-008 | Тест ошибки записи отчёта         | ERR-PY-010                           | пользователь получает fatal-ошибку записи     | нет в исходном примере |
| TEST-PY-009 | Тест ошибки записи лога           | ERR-PY-011                           | поведение при ошибке лога определено          | критичность неясна     |

### 4.13. Реестр открытых вопросов

| ID             | Вопрос                                                            | На что влияет                                    | Что блокирует                     | Статус |
| -------------- | ----------------------------------------------------------------- | ------------------------------------------------ | --------------------------------- | ------ |
| OQ-PY-DATA-001 | Какие колонки должны быть обязательными в CSV-отчёте?             | DATA-PY-010, REQ-PY-004, TEST-PY-004, INT-PY-003 | Technical Requirements            | open   |
| OQ-PY-RULE-001 | Как считать слова при пунктуации, числах и специальных символах?  | RULE-PY-005, REQ-PY-003, TEST-PY-003, MOD-PY-004 | Technical Requirements, Testing   | open   |
| OQ-PY-STOR-001 | При повторном запуске отчёт перезаписывается или создаётся новый? | STOR-PY-001, REQ-PY-004, Operation               | Technical Requirements, Operation | open   |
| OQ-PY-ERR-001  | Как система должна реагировать на пустую входную папку?           | ERR-PY-009, RULE-PY-009, TEST-PY-007             | Technical Requirements, Testing   | open   |

## 5. Пример структурированных фактов

Полный facts register пока не создаётся. Ниже минимальный пример, достаточный для проверки формы.

```yaml
facts:
  - id: FACT-PY-001
    subject: PRJ-PYFILE-001
    relation: contains
    object: REQ-PY-001
    source: SRC-PY-EX-001
    validation_status: valid

  - id: FACT-PY-002
    subject: REQ-PY-001
    relation: is_verified_by
    object: TEST-PY-001
    source: SRC-PY-EX-001
    validation_status: valid

  - id: FACT-PY-003
    subject: ENT-PY-003
    relation: contains
    object: DATA-PY-004
    source: SRC-PY-EX-001
    validation_status: valid

  - id: FACT-PY-004
    subject: RULE-PY-001
    relation: validates
    object: DATA-PY-001
    source: SRC-PY-Q-001
    validation_status: valid

  - id: FACT-PY-005
    subject: RULE-PY-001
    relation: raises
    object: ERR-PY-001
    source: SRC-PY-Q-001
    validation_status: valid

  - id: FACT-PY-006
    subject: EVENT-PY-001
    relation: triggers
    object: FLOW-PY-001
    source: SRC-PY-Q-001
    validation_status: valid

  - id: FACT-PY-007
    subject: MOD-PY-005
    relation: provides
    object: INT-PY-003
    source: SRC-PY-EX-001
    validation_status: valid

  - id: FACT-PY-008
    subject: OQ-PY-DATA-001
    relation: affects
    object: REQ-PY-004
    source: SRC-PY-Q-001
    validation_status: valid
```

Наблюдения:

- форма фактов подходит;
- для реальной генерации понадобится полный Facts Register;
- связь `is_verified_by` можно оставить как обратную проекцию для чтения, но основная машинная форма должна быть `TestCase verifies Requirement`;
- TestCase не должен задавать ожидаемое поведение вместо Requirement. Если проверка нужна, но Requirement неясен или отсутствует, нужно создавать `RequirementGap` и ставить TestCase в статус `pending_requirement`.

## 6. Проверка трассировки

### 6.1. Минимальная цепочка

| Requirement | Task | CodeArtifact | TestCase | Статус |
|---|---|---|---|---|
| REQ-PY-001 | TASK-PY-001 | CODE-PY-001 | TEST-PY-001 | planned |
| REQ-PY-002 | TASK-PY-002 | CODE-PY-002 | TEST-PY-002 | planned |
| REQ-PY-003 | TASK-PY-003 | CODE-PY-003 | TEST-PY-003 | blocked by OQ-PY-RULE-001 |
| REQ-PY-004 | TASK-PY-004 | CODE-PY-004 | TEST-PY-004 | blocked by OQ-PY-DATA-001, OQ-PY-STOR-001 |
| REQ-PY-005 | TASK-PY-005 | CODE-PY-005 | TEST-PY-005 | planned |
| REQ-PY-006 | TASK-PY-006 | CODE-PY-002 / CODE-PY-003 | TEST-PY-006 | planned |
| REQ-PY-007 | TASK-PY-007 | CODE-PY-002 | TEST-PY-007 | blocked by OQ-PY-ERR-001 |

Примечание: блокировки, связанные с неясным ожидаемым поведением, нужно уточнить как `RequirementGap`, а не оставлять только как общий `OpenQuestion`.

### 6.2. Планируемые задачи

| ID | Название | Реализует / закрывает | Ожидаемый результат |
|---|---|---|---|
| TASK-PY-001 | Реализовать проверку входной папки | REQ-PY-001 | проверка в ProcessingUseCase / CLI |
| TASK-PY-002 | Реализовать поиск `.txt` файлов | REQ-PY-002 | SVC-PY-002 FileDiscoveryService |
| TASK-PY-003 | Реализовать подсчёт статистики | REQ-PY-003 | SVC-PY-004 StatisticsService |
| TASK-PY-004 | Реализовать запись CSV-отчёта | REQ-PY-004 | SVC-PY-005 CsvReportService |
| TASK-PY-005 | Реализовать логирование ошибок | REQ-PY-005 | SVC-PY-006 LoggingService |
| TASK-PY-006 | Добавить тест неизменности исходных файлов | REQ-PY-006 | регрессионный тест |
| TASK-PY-007 | Принять решение и реализовать поведение при пустой папке | OQ-PY-ERR-001 | закрытое правило + тест |

### 6.3. Планируемые кодовые артефакты

| ID | Путь / артефакт | Реализует |
|---|---|---|
| CODE-PY-001 | `src/app/processing_use_case.py` | SVC-PY-001 / MOD-PY-001 |
| CODE-PY-002 | `src/infrastructure/file_scanner.py` | SVC-PY-002, SVC-PY-003 / MOD-PY-002 |
| CODE-PY-003 | `src/domain/statistics_service.py` | SVC-PY-004 / MOD-PY-003 |
| CODE-PY-004 | `src/infrastructure/csv_report_writer.py` | SVC-PY-005 / MOD-PY-004 |
| CODE-PY-005 | `src/infrastructure/logging_setup.py` | SVC-PY-006 / MOD-PY-005 |
| CODE-PY-006 | `src/main.py` | INT-PY-001 |

## 7. Проверка возможности SDD

### 7.1. Разделы, которые можно сформировать сейчас

| SDD section         | Статус   | Причина                                                          |
| ------------------- | -------- | ---------------------------------------------------------------- |
| `spec.md`           | можно    | границы проекта понятны                                          |
| `requirements.md`   | частично | четыре открытых вопроса блокируют полную техническую детализацию |
| `entities.md`       | можно    | основные сущности выделены                                       |
| `data-model.md`     | частично | есть разрывы по CSV-схеме и правилу подсчёта слов                |
| `rules.md`          | частично | не решены правило подсчёта слов и поведение пустой папки         |
| `errors.md`         | частично | не решены пустая папка и критичность ошибки записи лога          |
| `flows.md`          | можно    | основной поток понятен                                           |
| `interfaces.md`     | частично | output path в CLI недоописан                                     |
| `architecture.md`   | можно    | слои и модули достаточно понятны                                 |
| `tests.md`          | частично | часть тестов заблокирована открытыми вопросами                   |
| `traceability.md`   | можно    | gaps можно показать явно                                         |
| `tasks.md`          | можно    | задачи можно сформировать с блокерами                            |
| `open-questions.md` | можно    | открытые вопросы явно зафиксированы                              |

### 7.2. Вывод по SDD

Из модели можно собрать **draft SDD**, но его нельзя считать полным technical SDD до закрытия:

- OQ-PY-DATA-001;
- OQ-PY-RULE-001;
- OQ-PY-STOR-001;
- OQ-PY-ERR-001.

## 8. Проверка полезности метамодели

### 8.1. Элементы, которые оказались полезными

| Тип элемента       | Результат     |
| ------------------ | ------------- |
| Project            | полезен       |
| Requirement        | полезен       |
| Actor              | полезен       |
| Entity             | полезен       |
| DataField          | полезен       |
| Rule               | полезен       |
| Error              | полезен       |
| Event              | полезен       |
| Flow               | полезен       |
| Storage            | полезен       |
| Interface          | полезен       |
| Module             | полезен       |
| Service            | нужен для атомизации поведения |
| Layer              | полезен       |
| TestCase           | полезен       |
| Task               | полезен       |
| CodeArtifact       | полезен       |
| OpenQuestion       | очень полезен |
| RequirementGap     | нужен как уточнение |
| StructuredFact     | полезен       |
| Register           | полезен       |
| Traceability       | полезен       |
| SDD section / View | полезен       |

### 8.2. Элементы, которые не потребовались для простого примера

| Тип элемента | Причина |
|---|---|
| Integration | есть только доступ к файловой системе, пока достаточно Interface |
| ExtensionPoint | полезен для будущего развития, но не нужен для первого SDD |
| Viewpoint | концептуально полезен, но для маленького примера может оставаться неявным |
| Transformation | полезен как правило, но пока не нужен как конкретный экземпляр элемента |
| Configuration | появляется как будущая тема, но не является обязательной для текущей модели |

### 8.3. Возможные уточнения метамодели

1. Уточнить правило Requirement / TestCase:
   - `Requirement` задаёт ожидаемое поведение;
   - `TestCase verifies Requirement` является основной машинной формой;
   - `Requirement is_verified_by TestCase` можно использовать как обратную view-проекцию;
   - если проверка нужна, но Requirement неясен или отсутствует, создаётся `RequirementGap`, а TestCase получает статус `pending_requirement`.

2. Уточнить разделение Entity / Module / Service / CodeArtifact:
   - анкета перечисляет `FileScanner`, `FileReader`, `StatsCalculator`, `ReportWriter`, `Logger` как системные сущности;
   - после атомизации они должны рассматриваться как Service или CodeArtifact, а не как Entity;
   - Module должен группировать ответственность: ScanningModule, StatisticsModule, ReportingModule, LoggingModule.

3. Уточнить классификацию файловой системы:
   - Actor, Interface, Integration или Storage?
   - Для этого примера файловая система работает как внешний актор и интерфейс файлового доступа.

4. Уточнить, нужен ли `Output path` как отдельный DataField:
   - CLI имеет входную и выходную папку, но output path пока недоописан.

5. Уточнить поведение при пустой папке:
   - это реальный `RequirementGap`, а не проблема документации.

## 9. Результат проверки

### 9.1. Что подтверждает тест

- Рабочая форма метамодели может описать простую Python-утилиту.
- Модель не слишком абстрактна: из неё получаются конкретные реестры и трассировка.
- Открытые вопросы сохраняются и не угадываются.
- SDD можно получить как draft view.
- Разделение model и views полезно.
- Трассировка выявляет реальные блокеры до формирования технических требований.

### 9.2. Что тест не доказывает

- Он не доказывает универсальность метамодели.
- Он не доказывает применимость к промышленным, GUI, web или embedded-системам.
- Он не доказывает, что SDD можно полностью генерировать автоматически.
- Он не доказывает корректность всех relation types.
- Он не доказывает окончательность ID-политики.

## 10. Следующие действия

1. Переклассифицировать открытые вопросы Python-утилиты: где это обычный OpenQuestion, а где строгий RequirementGap.
2. Решить, как классифицировать системные сущности и модули.
3. Закрыть четыре открытых вопроса по Python-утилите через Requirements, Rules или rejected decisions.
4. Создать полный Facts Register для этого примера.
5. Сформировать draft SDD folder для этого примера.
6. Повторить validation на втором примере с GUI или template/export поведением.

## 11. Связанные документы

### Входные документы

- [[docs/08_digital_system_cad/metamodel/01_Model_Elements|Model Elements]]
  - Передаёт: типы элементов.
  - Используется для: извлечения элементов из примера.
  - Ограничение: остаётся рабочим кандидатом.

- [[docs/08_digital_system_cad/metamodel/02_Model_Relations|Model Relations]]
  - Передаёт: типы связей.
  - Используется для: фактов и трассировки.
  - Ограничение: обратные связи проверки требуют уточнения.

- [[docs/08_digital_system_cad/metamodel/07_SDD_From_Model|SDD From Model]]
  - Передаёт: отображение SDD-разделов.
  - Используется для: проверки возможности SDD.
  - Ограничение: в этом документе реальный SDD ещё не генерируется.

### Выходные документы

- будущий полный facts register для Python File Processing Utility;
- будущий draft SDD для Python File Processing Utility;
- будущие уточнения метамодели.

## 12. История изменений

- Initial version: создана первая проверка рабочей формы метамодели Digital System CAD на примере Python File Processing Utility: извлечены элементы, реестры, пример фактов, трассировка, проверка возможности SDD и заметки по уточнению метамодели.
- Updated: документ переведён на русский язык; технические ID, YAML-ключи и имена типов сохранены без изменения.
