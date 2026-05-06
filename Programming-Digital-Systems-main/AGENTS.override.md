# AGENTS.override.md

## 1. Назначение

Этот файл дополняет `AGENTS.md` правилами работы AI-агента с safety-relevant systems в контексте Digital System CAD.

Файл применяется, когда проект, документ, пример, модель или задача связаны с системами, где ошибка может привести к физическому, эксплуатационному, инфраструктурному, финансовому, медицинскому или иному критическому ущербу.

> [!info] Главное
> Safety не является внешним стоп-фактором. Safety является частью модели, SDD, тестов и Codex task pack.

## 2. Обязательный документ

Перед работой с safety-relevant content агент должен прочитать:

```text
docs/08_digital_system_cad/metamodel/08_Safety_As_Model_Layer.md
```

Этот документ определяет:

- Safety as Model Layer;
- SafetyRequirement;
- SafetyRule;
- SafetyGap;
- SafetyGate;
- P0 safety tests;
- правило `block unsafe paths, allow safe work`.

## 3. Главный принцип

Агент должен соблюдать принцип:

```text
Safety is not a blocker by default.
Unresolved critical safety behavior blocks unsafe execution paths only.
```

По-русски:

```text
SafetyGap не должен останавливать весь процесс разработки.
SafetyGap должен блокировать только опасную ветку работы.
```

## 4. Что агент должен делать

Если система safety-relevant, агент должен:

1. Выделить safety-relevant requirements.
2. Описать SafetyRequirement как профиль Requirement.
3. Описать SafetyRule как профиль Rule.
4. Описать CriticalEvent как профиль Event.
5. Описать FailsafeState как профиль State.
6. Описать SafetyError как профиль Error.
7. Создать или указать P0 SafetyTestCase.
8. Создать SafetyGap, если поведение safety-critical ситуации не определено.
9. Указать, какие tasks блокируются SafetyGap.
10. Указать, какие safe tasks разрешены несмотря на SafetyGap.
11. Не придумывать missing safety behavior без источника.
12. Формировать Codex task pack только для разрешённого model slice.

## 5. Что агенту запрещено

Агенту запрещено:

- игнорировать SafetyGap;
- превращать SafetyGap в полный стоп проекта;
- реализовывать unsafe execution path при unresolved SafetyGap;
- создавать real-world adapter без закрытых P0 safety tests;
- обходить SafetyRule ради ускорения разработки;
- генерировать автономное опасное поведение без утверждённых требований, правил и тестов;
- считать feature test заменой P0 safety test;
- считать SDD safety section источником правды, если он не связан с model facts.

## 6. Разрешённая работа при SafetyGap

Если SafetyGap существует, агент может продолжать только safe work:

- model refinement;
- simulation;
- state machine;
- validators;
- interface stubs;
- P0 safety tests;
- documentation;
- SDD transformation;
- Codex context generation;
- non-operational architecture skeleton.

## 7. Блокируемая работа при SafetyGap

SafetyGap должен блокировать:

- real-world actuator control;
- real flight adapter;
- production deployment;
- bypass of safety checks;
- unsafe autonomous behavior;
- tasks explicitly listed in `blocked_tasks`.

## 8. Приоритет тестов

Агент должен использовать приоритеты:

```text
P0 — Safety tests
P1 — Core behavior tests
P2 — Integration tests
P3 — UI / convenience tests
P4 — Optimization tests
```

Правило:

> P0 safety tests must exist before implementing behavior that depends on the related SafetyRule.

## 9. Codex task pack rule

Для safety-relevant task Codex context должен содержать:

```text
- related Requirements;
- related SafetyRequirements;
- related SafetyRules;
- related CriticalEvents;
- related FailsafeStates;
- related SafetyErrors;
- related SafetyGaps;
- P0 SafetyTestCases;
- blocked tasks;
- allowed tasks;
- forbidden behaviors;
- affected CodeArtifacts.
```

Если этих данных нет, агент должен создать OpenQuestion / SafetyGap, а не додумывать поведение.

## 10. История изменений

- Initial version: добавлены правила safety profile для AI-агента и Codex workflow.
