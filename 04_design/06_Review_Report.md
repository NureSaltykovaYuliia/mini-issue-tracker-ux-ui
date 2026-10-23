# 06 Review Report — Mini Issue Tracker (Release MVP), крок G6

| Поле | Значення |
| :--- | :--- |
| Дата | 2026-10-23 |
| Об'єкт перевірки | Figma-файл `OFbkJ1FsixY8G3CYzEsEsH` (сторінка `Page 1`), версія після ручного прототипування P1 |
| Еталон | `03_figma_prep/05_Figma_Brief_v1.0.md`, `01_requirements/01_Input_Pack_v1.0.md`, `01_requirements/Decision_Log.md`, методичка §§17–21 |
| Докази | 6 PNG у `04_design/screenshots/` (експорт 2x) + ручна перевірка prototype connections у вкладці Prototype |
| Хто виконав аудит | AI: ChatGPT Free (GPT-4o, аналіз зображень та текстового контракту за промптом G6) за участі Ходуса Данила (QA Auditor) |
| Статус | Завершений звіт аудиту. Зауваження розглянуто та зафіксовано командою (Контроль D виконано) |

> **Примітка щодо верифікації:** Звіт фіксує результати експертного аудиту візуальних контрактів та станів інтерфейсу (крок G6). Наскрізні сценарії взаємодії та поведінка переходів верифіковані вручну в режимі Present і задокументовані у протоколі `05_qa/Test_Cases_T01_T10.md`.

## 0. Видимі Screen/State IDs і читабельність

| Файл | Screen/State ID | Текст читається? | Примітка |
| :--- | :--- | :--- | :--- |
| `S-01_auth.png` | S-01 | Так | Лише placeholder «Authentication boundary» |
| `S-02-A_all_list.png` | S-02-A | Так | 5 рядків ISS-101…105 |
| `S-02-B_important_list.png` | S-02-B | Так | 1 рядок ISS-101 |
| `S-02-C_empty_list.png` | S-02-C | Так | Контекст All, порожнє тіло таблиці |
| `M-01_create_issue.png` | M-01 (над S-02-A) | Так; таблиця під модалкою частково перекрита (очікувано) | Заповнений валідний приклад |
| `S-03_issue_details.png` | S-03 | Так | Контекст «Team Member — assignee (Team Member A)», ISS-101 |

**Не надано в цьому експорті** (фрейми існують у файлі за назвами шарів, але PNG не вивантажено: через добовий ліміт завантаження медіа ChatGPT Free аудит проведено за 6 ключовими PNG):
`Reference · Permissions and controls`, `Reference · Status transitions`, `Reference · Important fixtures`, `Reference · Successful creation result`, `Reference · Empty and error cases`, `Reference · Transition intent`, `Reference · Blockers and scope`, `Local components`.
Через це аудит **частковий**: вимоги, доказ яких лежить у цих фреймах, позначено NOT VERIFIABLE, а не FAIL. Це не доведена відсутність стану у файлі.

## Частина A — вимоги

Легенда: PASS — очікуваний UI-доказ видно; PARTIAL — видно частину; FAIL — видно суперечність; NV — NOT VERIFIABLE.

### US-01 — Create Issue

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AC-01.1 | Можна ввести Title і Description | M-01 | Поля Title і Description із заповненими значеннями; інших полів вводу немає | PASS | Реальне введення: реалізація |
| AC-01.2 | Title обов'язковий, «Title is required» | M-01 | Лише текст анотації; error state у PNG не показано | PARTIAL | Експорт `Empty and error cases`; T-02 |
| AC-01.3 | Description обов'язковий | M-01 | Лише анотація; error state не показано; текст помилки не визначено (Q-08) | PARTIAL | Як вище |
| AC-01.4 | Після створення: ID, Open, created_at, author | Successful creation ref; прототип M-01 → S-03 | Ref не експортовано. Прототип після Create відкриває S-03 з **ISS-101 / Resolved / High**, а не нову issue | PARTIAL (статика NV, прототип суперечить) | DEF-10; унікальність ID — реалізація |
| AC-01.5 | Priority не встановлено | Successful creation ref | Не експортовано | NV | T-01 |

### US-02 — View Issues

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AC-02.1 | Автентифікований користувач бачить список | S-02-A | Список із 5 issues | PASS (UI) | Автентифікація — лише реалізація |
| AC-02.2 | ID, Title, Status, Priority, Assignee (якщо є) | S-02-A/B | Усі 5 колонок; ISS-103 має `[ ]` для відсутніх Priority/Assignee | PASS | Остаточна копія для відсутнього значення (D-03) |
| AC-02.3 | Вибрати issue → деталі | S-02-A/B → S-03 | Підкреслені Title; prototype reactions на рядках ведуть на S-03 | PARTIAL | Усі рядки відкривають S-03 з даними ISS-101 (DEF-11); T-09 |
| AC-02.4 | Деталі: ID, Title, Description, Status, Priority, Assignee, Author, Created at | S-03 | Усі 8 полів видно; Created at = `[timestamp]` | PASS | Формат дати (Q-09) |
| AC-02.5 | Порожній список або повідомлення | S-02-C | Порожнє тіло таблиці із заголовками | PASS | UX-04 |

### US-03 — Assign Issue (критерії без ID у джерелі)

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| US-03, критерій 1 | Можна вибрати одного assignee | S-03 (Lead) | У показаному контексті Team Member поле лише для читання; контрол вибору не видно | NV | Експорт `Permissions and controls`; T-03 |
| US-03, критерій 2 | Assignee — член команди | S-03 / ref | Не показано | NV | T-03; серверна перевірка |
| US-03, критерій 3 | Призначає лише Team Lead | S-03 | Для Team Member контролу призначення немає (read-only) | PARTIAL | Контекст Team Lead не експортовано |
| US-03, критерій 4 | Поточний assignee видно | S-03, S-02-A | «Assignee: Team Member A» у S-03 і в списку | PASS | — |

### US-04 — Set Priority

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AC-04.1 | Значення Low, Normal, High, Critical | S-02-A | Усі чотири значення у даних; селектор не показано | PARTIAL | T-04 |
| AC-04.2 | Змінює лише Team Lead | S-03 | Team Member: Priority read-only | PARTIAL | Контекст Lead не експортовано |

### US-05 — Track Status

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AC-05.1 | Status видно для кожної issue | S-02-A | Колонка Status заповнена в кожному рядку | PASS | — |
| AC-05.2 | Status на сторінці issue | S-03 | Секція Status з бейджем `Resolved` | PASS | — |
| AC-05.3 | Status у списку | S-02-A/B | Так | PASS | — |

### US-06 — Comments

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AC-06.1 | Порожній comment не створюється | S-03 / error ref | Не показано | NV | T-07 |
| AC-06.2 | Comment зберігається й відображається | S-03 | Намальовано один збережений comment | PARTIAL | Persistence — лише реалізація |
| AC-06.3 | Автор видно | S-03 | «Team Member A» | PASS (UI) | Persistence — реалізація |
| AC-06.4 | Дата/час видно | S-03 | `[timestamp]` (Q-09) | PARTIAL | Формат |
| AC-06.5 | Помилка save → comment не створено | S-03 / error ref | Не показано | NV | T-07 |

### US-07 — Update Status

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AC-07.1 | Нова issue — Open | Successful creation ref | Не експортовано | NV | T-01 |
| AC-07.2 | Open, In Progress, Resolved, Closed | S-02-A | Усі 4 статуси в даних | PASS | — |
| AC-07.3 | Новий статус зберігається | — | Не перевіряється макетом | NV | Реалізація |
| AC-07.4 | Не-assignee не змінює status | S-03 / permissions ref | Показано лише контекст assignee | NV | T-05, T-06 |
| AC-07.5 | Лише допустимі значення / переходи | S-03 | Для `Resolved` доступні тільки `In Progress` і `Closed` (BR-08.1 виконано для цього стану) | PARTIAL | Інші 3 стани — `Status transitions` ref |

### US-08 — Important Issues

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AC-08.1 | High + не Closed → входить | S-02-B | ISS-101 High/Resolved присутня | PASS | — |
| AC-08.2 | Critical + не Closed → входить | S-02-B | У даних немає жодної Critical + не Closed issue; доказу немає | NV (прогалина даних) | DEF-13; T-08 |
| AC-08.3 | Low/Normal не входять | S-02-B | ISS-104 Normal і ISS-105 Low відсутні | PASS | — |
| AC-08.4 | Closed не входить незалежно від priority | S-02-B | ISS-102 Critical/Closed відсутня | PASS | — |

### UI-релевантні BR і D-рішення

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
| :--- | :--- | :--- | :--- | :--- | :--- |
| BR-03 | Початковий status Open | Successful creation ref | Не експортовано | NV | T-01 |
| BR-04 / BR-05 | Відсутність priority ≠ рівень; лише 4 рівні | S-02-A | ISS-103 показано як `[ ]`, а не вибраний рівень | PARTIAL | Копія «Not Set» (D-03) |
| BR-06 | Priority змінює лише Lead | S-03 | Як AC-04.2 | PARTIAL | — |
| BR-08 / BR-08.1 | Status змінює лише assignee; 4 переходи; Closed без виходу | S-03 | Видно тільки Resolved → {In Progress, Closed} | PARTIAL | `Status transitions` ref |
| BR-09 / BR-09.1 | High/Critical AND status != Closed; Resolved лишається | S-02-B | Анотація з точним предикатом; ISS-101 Resolved включено | PASS | — |
| D-01 | Desktop, grayscale, tabs All/Important, Create — modal | Усі | Виконано | PASS | Статус D-01 у Decision Log не APPROVED |
| D-02 | S-01 лише межа автентифікації | S-01 | Без полів логіна | PASS | — |
| D-03 | Відсутній priority = «Not Set» | S-02-A | Використано `[ ]` | PARTIAL | Рішення не затверджене |
| D-05 | Заборонені controls — disabled, не приховані | S-03 | Для Team Member Assignee/Priority — просто текст, disabled-контролу немає | PARTIAL | Q: чи затверджено D-05 |
| D-06 | Вибір → Apply біля контролу | S-03 | Кнопок Apply немає; переходи статусу — окремі кнопки | NV / не представлено | Q: статус D-06 |
| D-07 | Повернення зберігає попередню вкладку | Прототип S-03 → S-02-A | Return завжди веде на S-02-A, навіть якщо прийшли з S-02-B | FAIL (якщо D-07 затверджено) | DEF-14 |
| D-08 | Фіктивні дані, симуляція | Усі | Анотації «fixture», «[timestamp]» | PASS | — |

### Окремі перевірки

| Перевірка | Результат |
| :--- | :--- |
| Права (4 контексти role/assignee) | Видно лише «Team Member — assignee». Інші 3 контексти — NV у цьому експорті |
| Current assignee | PASS (S-03, список) |
| Початкові значення (Open, Not Set, author, created_at) | NV (ref не експортовано); прототипний маршрут Create суперечить (DEF-10) |
| Чотири дозволені переходи | Видно 2 з 4 (з Resolved). Closed без виходу — NV |
| Resolved != Closed | PASS (ISS-101 Resolved у Important, ISS-102 Closed — ні) |
| Important predicate | PASS для High/Resolved, Critical/Closed, Low, Normal, Not Set; Critical + не Closed — немає прикладу |
| Comments | Успішний вигляд PARTIAL; empty та save-error — NV |
| Validation / empty states | Empty All — PASS; validation — NV |
| Зайві функції (delete, attachments, bulk, row selection, history) | Не виявлено — PASS |
| Page icon placeholders / декоративні квадрати | Не виявлено. Але `[ ]` у даних і в label коментаря візуально схоже на checkbox (UX-01) |
| HTTPS, backup, response time, login | NOT VERIFIABLE за зображенням |

## Частина B — UX (до 5 доказових проблем)

> Це експертний огляд зображень, а не сертифікація доступності й не тест із реальними користувачами.

| UX-ID | Категорія | Доказ | Чому це проблема |
| :--- | :--- | :--- | :--- |
| UX-01 | Читабельність | `[ ]` у Priority/Assignee для ISS-103 і як label поля коментаря на S-03 | Виглядає як порожній checkbox; методичка §8 прямо застерігає від цього |
| UX-02 | Зрозумілість дій | На S-03 кнопки `In Progress` / `Closed` стоять під бейджем `Resolved` без дієслова чи підпису | Важко відрізнити дію «змінити на…» від відображення значення; той самий стиль, що й таби All/Important |
| UX-03 | Error prevention / навігація | У M-01 немає Cancel/Close | Користувач не може відмовитися від створення; у прототипі overlay може не закриватися (DEF-12) |
| UX-04 | Зрозумілість стану | S-02-C — порожня таблиця без повідомлення | Візуально не відрізняється від стану «ще завантажується» чи помилки завантаження. AC-02.5 це допускає, тому це UX, а не DEF |
| UX-05 | Навігація / consistency | `[action]` як підпис кнопки збереження коментаря; Return завжди веде на All | Незрозуміло, що робить кнопка; втрачається контекст Important |

## Частина C — дефекти та UX-зауваження

| ID | Severity | Location | Source | Evidence | Minimal correction |
| :--- | :--- | :--- | :--- | :--- | :--- |
| DEF-10 | Major | Прототип: M-01 `Create` → S-03 | AC-01.4, AC-01.5, AC-07.1; методичка §17 | Після Create відкривається ISS-101 Resolved/High замість нової issue (Open, Not Set) | Вести `Create` на фрейм `Reference · Successful creation result` або на копію стану S-03 з даними нової issue; або прибрати лінк до рішення D-06 |
| DEF-11 | Major | Прототип: рядки ISS-102…105 на S-02-A → S-03 | AC-02.3; методичка §17 («дані мають збігатися за ID») | Будь-який рядок відкриває S-03 з ISS-101 | Лишити hotspot лише на ISS-101 або підписати S-03 як спільний шаблон для решти рядків |
| DEF-12 | Major | M-01 overlay | Методичка §8, §17 (Cancel → попередній S-02); T-09 | У M-01 немає Cancel/Close; overlay-дія не має `close on click outside` | Увімкнути «Close when clicking outside» для overlay. Cancel додати лише після рішення про close/cancel (Brief §13, BLOCKER) |
| DEF-13 | Medium | Набір fixtures (S-02-A/B) | AC-08.2; методичка §20 (ISS-001…ISS-008) | Немає Critical + не Closed issue; ID не збігаються з набором методички (у завданні фігурує ISS-003) | Додати рядок Critical + Open/In Progress або перейти на набір §20 |
| DEF-14 | Minor | Прототип: S-03 `Return to Issues List` | D-07 (не затверджено) | Завжди повертає на S-02-A | Після затвердження D-07: окремий маршрут з S-02-B або «Back» (Navigate back) |
| DEF-15 | Minor | Overlay M-01 | Методичка §8 («не змішуйте продукт і пояснення») | Overlay — це весь фрейм M-01 разом із заголовком-анотацією та копією списку | Винести модалку в окремий фрейм лише з `Create Issue modal` і використовувати його як overlay |
| DEF-16 | Major (процес) | `01_requirements/Decision_Log.md` | Методичка §6, Контроль B | Жодне з D-01…D-08 не має статусу APPROVED, лише «Погодити…» | Внести рішення людини (APPROVED/REJECTED, хто, дата) |
| UX-01 | Minor | S-02-A ISS-103; S-03 label коментаря | Методичка §8 | `[ ]` схоже на checkbox | Після D-03 замінити на «Not Set» / «—» / підпис «Comment» |
| UX-02 | Minor | S-03 Status | — | Кнопки переходів без підпису дії | Додати підпис «Change status to:» або подібний (копія не визначена — Q-08) |
| UX-04 | Minor | S-02-C | AC-02.5 | Порожня таблиця без повідомлення | Опційно: нейтральне повідомлення після рішення Q-18 |
| UX-05 | Minor | S-03 comment action | Q-08 | `[action]` | Визначити підпис після Q-08 |

## Завершення

1. **UI design coverage — partial.** Видимі екрани покривають список, деталі, Important, порожній стан і create-форму. Validation, comment errors, 3 з 4 рольових контекстів, переходи статусів і результат створення лише в неекспортованих reference-фреймах. Окремо бракує Critical + не Closed.
2. **Prototype evidence — verified у Present.** Прототип перевірено вручну в режимі Present тестувальником Вдовенком Олегом за сценаріями T-01..T-10 (див. `05_qa/Test_Cases_T01_T10.md`). Всі базові навігаційні переходи успішно підтверджено з урахуванням меж низькобюджетного навчального прототипу.
3. **Implementation tests outstanding:** persistence issue/comment/status (AC-06.2, AC-07.3), унікальність ID (AC-01.4), серверна авторизація (AC-04.2, AC-07.4, US-03 крит. 3), валідація на сервері (AC-01.2/01.3, AC-06.1), помилка збереження (AC-06.5), автентифікація (AC-02.1), формат часу (Q-09), HTTPS, backup, час відповіді.

Загального висновку «усі AC виконано» немає: є NV-пункти, які вимагають реалізації в коді продукту.

## Контроль D — рішення студента

| ID | Статус (Контроль D) | Причина та інженерне рішення команди | Хто погодив | Дата |
| :--- | :--- | :--- | :--- | :--- |
| **DEF-10** | **ACCEPTED** (межа симуляції) | Відкриття підготовленого екрана деталей є узгодженою межею прототипу Starter (D-08). Для динамічного створення нового запису потрібні Figma variables, недоступні у Free. Поведінку зафіксовано в тесті T-01. | Кузнецов Герман (QA Lead) | 2026-10-23 |
| **DEF-11** | **ACCEPTED** (шаблон перегляду) | Екран S-03 є спільним канонічним шаблоном перегляду деталей у low-fi макеті. Узгоджено як допустиму демонстраційну форму (D-08). | Бєлікова Марина (UX-архітектор) | 2026-10-23 |
| **DEF-12** | **MITIGATED** (виправлено у Figma) | Шар backdrop розділено на смуги з Close overlay навколо вікна; додано кнопку Cancel. Скасування модалки верифіковано в тесті T-09. | Ходус Данило (Prototyping Lead) | 2026-10-23 |
| **DEF-13** | **ACCEPTED** (предикат доведено) | Логіку Important predicate верифіковано на станах High/Resolved, Critical/Closed, Normal, Low, Not Set. Відсутність Critical+Open не порушує математичну коректність фільтра (T-08). | Вдовенко Олег (Аналітик/QA) | 2026-10-23 |
| **DEF-14** | **ACCEPTED** (базовий маршрут) | Повернення Return to Issues List на S-02-A відповідає базовій лінійній структурі прототипу без збереження динамічної історії (D-07). | Ходус Данило (Prototyping Lead) | 2026-10-23 |
| **DEF-15** | **MITIGATED** (візуальна чистка) | Службові анотації та копії списку розміщено за межами продуктового фрейму в Review notes (REF-01) відповідно до §8 методички. | Салтикова Юлія (Figma Designer) | 2026-10-23 |
| **DEF-16** | **MITIGATED** (затверджено рішення) | Документ Decision_Log.md оновлено та переведено у статус APPROVED (D-01..D-08) за підписами команди від 2026-10-22. Блокери знято. | Кузнецов Герман (QA Lead) | 2026-10-23 |
| **UX-01** | **ACCEPTED** (уточнено контракт) | Зафіксовано у D-03 та Screen Contracts, що [ ] є текстовим маркером відсутності значення (Not Set / Unassigned), а не інтерактивним чекбоксом. | Салтикова Юлія (Figma Designer) | 2026-10-23 |
| **UX-02** | **ACCEPTED** (канонічні кнопки) | Кнопки зміни статусу відображають дозволені переходи BR-08.1 з поточного стану Resolved (In Progress, Closed). | Бєлікова Марина (UX-архітектор) | 2026-10-23 |
| **UX-04** | **ACCEPTED** (відповідність AC) | Порожня таблиця без тексту повідомлення відповідає вихідному AC-02.5. | Вдовенко Олег (Аналітик/QA) | 2026-10-23 |
| **UX-05** | **ACCEPTED** (підпис кнопки) | Дія коментаря задокументована як збереження коментаря за US-06; текстовий лейбл кнопки уніфіковано в брифі v1.0. | Ходус Данило (Prototyping Lead) | 2026-10-23 |

**Зміни, внесені після цього AI-аудиту:**
1. Повністю узгоджено та переведено в статус `APPROVED` проєктні рішення у `01_requirements/Decision_Log.md`.
2. Оновлено `03_figma_prep/05_Figma_Brief_v1.0.md` на офіційний затверджений бриф v1.0 згідно з Додатком A.
3. Проведено та задокументовано 10 ручних тестів T-01..T-10 у `05_qa/Test_Cases_T01_T10.md`, включаючи мінітест з одногрупником.
4. Оновлено реєстр дефектів `05_qa/Defect_Change_Log.md`: дефекти DEF-10..DEF-16 та зауваження UX переведено зі статусу `OPEN` у `CLOSED / MITIGATED` із фіксацією обґрунтування.
5. Усунено суперечності в `05_qa/AI_Interaction_Log.md` щодо назви інструмента аудиту (ChatGPT Free / GPT-4o) та статусу проходження тестів.
