# Test Cases T-01 – T-10 — Mini Issue Tracker (прототип Figma)

| Поле | Значення |
| :--- | :--- |
| **Об'єкт** | Figma-файл `OFbkJ1FsixY8G3CYzEsEsH`, сторінка `Page 1`, flow «Issues flow» зі стартом на `S-02-A` |
| **Джерело тестів** | Методичні рекомендації §17, §20, §21; Brief v1.0; `02_architecture/03_Screen_Contracts.md`; `04_design/06_Review_Report.md` |
| **Перше проходження** | 2026-10-23: Вдовенко Олег (QA Tester), Ходус Данило (Prototyping Lead) |
| **Перегляд після зауважень викладача** | Листопад 2026: стан prototype connections і кадрів перевірено читанням Figma-файлу (без змін); статуси нижче відповідають цьому стану |

> **Правило доказу (Screen Contracts §10.2).** PASS ставиться лише для стану, який реально показано: на експортованому кадрі (`04_design/screenshots/`) або в пройденому маршруті прототипу. Текст контракту доводить, що вимогу *записано*, а не що її *показано*. Непоказаний стан має статус NOT RUN. Відповідно до D-08 прототип не доводить серверне збереження, авторизацію сесій чи транзакції.
>
> Статуси: **PASS** — очікуваний результат показано; **PARTIAL** — показано частину; **FAIL** — показано суперечність очікуванню; **NOT RUN** — доказу немає.

---

## Prototype connections (стан Figma-файлу, листопад 2026)

| # | Звідки | Trigger → Action | Куди | Зауваження |
| :--- | :--- | :--- | :--- | :--- |
| **P-1** | S-02-A / таб `Important` | On click → Navigate | S-02-B | Працює |
| **P-2** | S-02-B / таб `All` | On click → Navigate | S-02-A | Працює |
| **P-3** | S-02-A / `Create Issue` | On click → Open overlay | M-01 | Працює |
| **P-4** | S-02-B / `Create Issue` | On click → Open overlay | M-01 | Працює |
| **P-5** | M-01 / `Create` (вузол `3:6282`) | On click → Navigate | S-03 · New issue ISS-106 (after Create), кадр `65:97` | Виправлено в листопаді 2026 (DEF-10): раніше вела на спільний S-03 з даними ISS-101 |
| **P-6** | S-02-A / шість рядків ISS-101…ISS-107; S-02-B / рядки ISS-101 і ISS-107 | On click → Navigate | S-03 · кадр свого ID (`3:5407`, `86:102`, `86:159`, `86:216`, `86:275`, `86:334`) | Виправлено 24.11.2026 (DEF-11): кожен рядок відкриває дані своєї issue |
| **P-7** | S-03 (спільний і новий) / `← Return to Issues List` | On click → Navigate | S-02-A | Працює; з S-02-B теж веде на S-02-A (DEF-14, D-07) |
| **P-8** | M-01 / `Cancel` (`40:97`) | On click → Close overlay | попередній список | Працює; issue не створюється |
| **P-9** | M-01 / чотири смуги `Modal backdrop` | On click → Close overlay | попередній список | Працює; клік у вікні форми не закриває її |

S-01 → S-02 переходу немає навмисно (D-02: демо починається з S-02).

---

## Протокол тестів

Для кожного тесту окремо вказано три рівні доказу: **К** — текст контракту, **М** — видимий стан макета, **П** — маршрут прототипу.

| ID | Очікуваний результат (методичка / Contracts) | Що показано | Статус | Що потрібно для PASS |
| :--- | :--- | :--- | :--- | :--- |
| **T-01**<br>Create<br>US-01; AC-01.1, 01.4, 01.5; AC-07.1; §17 | У M-01 лише Title і Description. Після `Create` показано підготовлений екран **нової** issue: введені Title/Description, Status = Open, Priority = Not Set, Assignee = Unassigned, ID відмінний від існуючих | **К:** CR-01, CR-05, CR-08. **М:** M-01 має два поля й Create/Cancel (`M-01_create_issue.png`). **П:** у Present `S-02-A → Create Issue → Create` відкриває ISS-106 «Review keyboard focus»: Open, Not Set, Unassigned, без коментарів (`S-03_new_issue_after_create.png`) | **PASS** | — |
| **T-02**<br>Validation<br>AC-01.2, 01.3 | Порожній Title → «Title is required», issue не створюється; порожній Description → створення блокується | **М:** `REF_empty_error_cases.png`, випадки 03 («Title is required») і 04 («Description is required», демонстраційний текст) | **PASS** (макет; прототипного маршруту немає) | — |
| **T-03**<br>Assignment<br>US-03, критерії 1–4; D-04 | Member не призначає (контроль недоступний); Team Lead обирає одного члена команди й може перепризначити; поточний assignee видно | **М:** `REF_permissions_4_contexts.png`: матриця для 4 контекстів і контроль призначення (Unassigned → Team Member A / B); `S-03_issue_details.png`: Member бачить Assignee лише як текст | **PASS** | — |
| **T-04**<br>Priority<br>AC-04.1, 04.2 | Member не змінює; Team Lead обирає лише Low/Normal/High/Critical; `Not Set` не вибирається | **М:** `REF_permissions_4_contexts.png`: контроль Priority з чотирма значеннями, `Not Set` не пропонується; `S-03_issue_details.png`: Member бачить Priority як текст | **PASS** | — |
| **T-05**<br>Status<br>AC-07.2, 07.5; BR-08.1 | Для assignee показано всі чотири дозволені переходи; заборонені недоступні; Closed без вихідних дій | **М:** `REF_status_transitions.png`: Open → In Progress; In Progress → Resolved; Resolved → In Progress або Closed; Closed — «No outgoing transition». **П:** у Present ISS-104 (In Progress) показує лише `Resolved`; ISS-107 (Open) — лише `In Progress`. Заборонені переходи подано відсутністю контролів | **PASS** | — |
| **T-06**<br>Lead restriction<br>AC-07.4; BR-08 | Team Lead, що не є assignee, не має активного керування статусом | **М:** `S-03_lead_non_assignee.png`: контекст Team Lead non-assignee, статус Open без контролів переходу; матриця (`REF_permissions_4_contexts.png`) і випадок 07 (`REF_empty_error_cases.png`, «Only the assignee can change the status.») | **PASS** | — |
| **T-07**<br>Comments<br>AC-06.1–06.5 | Збережений коментар має author і date/time; порожній коментар не створюється; невдале збереження показує помилку й не створює коментар | **М:** `S-03_issue_details.png`: збережений коментар «Team Member A · 2026-10-23 14:20»; `REF_empty_error_cases.png`: випадок 05 (порожнє поле, коментар не створюється), випадок 06 («Comment was not saved. Try again.», коментаря немає) | **PASS** | — |
| **T-08**<br>Important<br>AC-08.1–08.4; BR-09.1 | У Important лише High/Critical зі status ≠ Closed (зокрема High+Resolved і Critical+Open); Closed, Low, Normal, Not Set відсутні; набір даних відрізняє правильне правило від хибного | **П:** у Present вкладка Important показує ISS-101 (High, Resolved) і ISS-107 (Critical, Open); ISS-102 (Critical, Closed), ISS-103 (Not Set), ISS-104 (Normal), ISS-105 (Low) відсутні (`S-02-B_important_list.png`, `REF_important_fixtures.png`) | **PASS** | — |
| **T-09**<br>Navigation<br>AC-02.3; D-07; §17 | Відкрити issue → її деталі; Return → список; Cancel/backdrop закриває M-01 без створення; дані на S-03 збігаються з вибраною issue | **П:** у Present: список → ISS-104 (дані ISS-104) → Return → список; Create Issue → M-01 → Create → ISS-106; Important → ISS-107 (дані ISS-107). Cancel і backdrop підключено до `Close overlay` (перевірено в Present 23.10.2026 і за prototype connections). Return завжди веде на S-02-A (обмеження, дозволене D-07) | **PASS** (з обмеженням D-07) | — |
| **T-10**<br>Scope<br>§8, §11 Brief | Немає delete, attachments, AI, історії змін, search, sorting, pagination, bulk і row selection, декоративних елементів | **М:** огляд 11 експортованих кадрів у `04_design/screenshots/`: заборонених функцій немає; плейсхолдерів `[ ]`, `[action]`, `[timestamp]` у продуктових екранах немає | **PASS** | — |

---

## Мінітест з одногрупником (§21 методичних рекомендацій)

Проведено 2026-10-23 (оператор — Ходус Данило, учасник — Вдовенко Олег). Завдання виконувалися без підказок.

| Завдання | Маршрут | Спостереження |
| :--- | :--- | :--- |
| 1. Створити заявку | S-02-A → `Create Issue` → M-01 → `Create` → S-03 | Кнопку створення знайдено одразу; скасування працює кліком по фону й кнопкою `Cancel`. Після `Create` тоді відкрилась issue ISS-101, а не нова; це виправлено 24.11.2026 (DEF-10) |
| 2. Знайти важливу Resolved-заявку | S-02-A → `Important` → ISS-101 → S-03 | Без вагань; ISS-101 High + Resolved залишається в Important, бо не Closed |
| 3. Пояснити, чому користувач не може змінити status | S-03 під контекстом non-assignee | Учасник пояснив правило (AC-07.4, BR-08) |

**Обмеження мінітесту.** Учасник — аналітик вимог, який знає правила, тому тест слабо показує зрозумілість інтерфейсу для непідготовленого користувача. Висновок стосується лише цього проходження. Для повторного мінітесту бажано залучити людину, яка не брала участі в проєкті.

---

## Підсумок

| Статус | Тести |
| :--- | :--- |
| PASS | T-01 … T-10 (T-09 з обмеженням D-07) |
| PARTIAL | — |
| FAIL | — |
| NOT RUN | — |

Перше проходження 23.10.2026 виконали Вдовенко Олег і Ходус Данило; повторну перевірку після зауважень викладача виконано 24.11.2026 у Figma Desktop (Present) з використанням AI-інструменту; результат прийняли Ходус Данило і Вдовенко Олег. Контрольне повторне проходження T-01, T-08, T-09 (список із 6 рядків; Important лише ISS-101 і ISS-107; рядок ISS-104 відкриває свою issue, Return → S-02-A; Create → ISS-106; Cancel закриває M-01 без створення) виконано 24.11.2026 у Present з використанням AI-інструменту; відповідальні за результат — Ходус Данило, Вдовенко Олег (PASS). Усі дефекти з реєстру закриті (`05_qa/Defect_Change_Log.md`); рішення D-09 і D-10 затверджено в `Decision_Log.md` (2026-11-24).
