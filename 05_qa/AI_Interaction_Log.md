# AI Interaction Log — Mini Issue Tracker UX/UI

Формат — методичні рекомендації, Додаток B2. Журнал фіксує всі запити до ШІ-інструментів, використані контексти, прийняті рішення, перевірку та фактичні обмеження. Усі текстові та аналітичні кроки виконані в **ChatGPT Free (GPT-4o)**, а генерація дизайну — у **Figma Agent (Starter)** відповідно до регламенту заняття.

---

## 👥 Склад команди та розподіл ролей

| Учасник команди | Роль у проєктуванні | Виконані кроки та обов'язки |
| :--- | :--- | :--- |
| **Вдовенко Олег** | Аналітик вимог / QA Tester | Відбір вимог (G1), верифікація Traceability, проведення ручних тестів прототипу (T-01..T-10) та мінітесту |
| **Бєлікова Марина** | UX-архітектор | План екранів (G2), формалізація контрактів екранів та матриць прав і переходів (G3) |
| **Кузнецов Герман** | Team Lead / Prompt Engineer | Ведення Decision Log, критичний аудит плану (G4), збірка англомовного брифу Figma (G5) |
| **Салтикова Юлія** | Figma Designer | Генерація макетів у Figma Agent (F1), візуальна корекція шарів та Auto Layout (F2) |
| **Ходус Данило** | QA Auditor / Prototyping Lead | Прототипування (P1), експорт скріншотів та фінальний аудит (G6) через ChatGPT Free |

---

## 📊 Зведена таблиця взаємодій з ШІ

| # | Date / operator / step | Tool / plan / mode | Context / version | Prompt / response | Decision / evidence | Limit / fallback |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | 2026-10-22 / Вдовенко Олег / G1 | ChatGPT Free / GPT-4o / стандартний текстовий | `SD_Spec.docx` (§0–§8) | Промпт G1 (текст нижче) → `01_Input_Pack_v1.0.md` | Помилка ШІ: ChatGPT включив US-09 (Attach files) до MVP. Після ручного Контролю A за §8 US-09 вилучено як Deferred; SR-10/11 (Future) виключено. Зафіксовано 8 US, 33 AC | 3 завантаження файлів/день; ліміт не вичерпано |
| **2** | 2026-10-22 / Бєлікова Марина / G2 | ChatGPT Free / GPT-4o / стандартний текстовий | Input Pack v1.0 + Decision Log | Промпт G2 (текст нижче) → `02_Screen_Map.md` | Помилка ШІ: окремі сторінки для priority, comments та призначення — відхилено. Об'єднано в S-03; список S-02 зі станами All / Important / Empty; модалка M-01 | не показано |
| **3** | 2026-10-22 / Бєлікова Марина / G3 | ChatGPT Free / GPT-4o / стандартний текстовий | Pack, D-Log, Screen Map | Промпт G3 (текст нижче) → `03_Screen_Contracts.md` | Згенеровано контракти екранів, Матрицю дозволів (4 контексти), Матрицю переходів BR-08.1 та Traceability | не показано |
| **4** | 2026-10-22 / Кузнецов Герман / G4 | ChatGPT Free / GPT-4o / режим рецензента | Pack, Contracts, Traceability | Промпт G4 (текст нижче) → `04_Plan_Review.md` | Виявлено 9 дефектів DEF-01…DEF-09 (зокрема DEF-08: форма логіна з паролем на S-01 всупереч Q-07). Затверджено D-01..D-08 (APPROVED) | не показано |
| **5** | 2026-10-22 / Кузнецов Герман / G5 | ChatGPT Free / GPT-4o / текстовий | Затверджені Pack, Contracts, Decision Log (APPROVED) | Промпт G5 (текст нижче) → `05_Figma_Brief_v1.0.md` | Сформовано англомовний бриф для Figma; Контроль C пройдено | не показано |
| **6** | 2026-10-22 / Салтикова Юлія / F1 | Figma Agent / Starter beta | `05_Figma_Brief_v1.0.md` | Launcher F1 (текст нижче) → згенеровано фрейми S-01…S-03, reference-панелі та компоненти | Збережено локальну копію-бекап `04_design/BEFORE_REVIEW.fig` | Використано AI-кредити Figma Starter |
| **7** | 2026-10-23 / Салтикова Юлія / F2 | Figma / Ручна корекція | Виділені frames у Figma | Launcher F2 (текст нижче) / Ручні правки шарів та Auto Layout згідно з F2-checklist | Вручну видалено порожні квадратні рамки біля заголовків екранів; службові примітки винесено за межі UI у REF-01; Auto Layout за 8-px сіткою | Денний ліміт AI-кредитів Figma; перехід на ручний fallback |
| **8** | 2026-10-23 / Ходус Данило / P1 | ChatGPT Free / GPT-4o | Figma file + Brief v1.0 | Запит на оптимізацію схеми prototype interactions → сформовано схему P1 | Figma Agent (Starter) не будує prototype connections — усі 7 маршрутів P-1..P-7 з'єднано вручну у вкладці Prototype | не показано |
| **9** | 2026-10-23 / Ходус Данило / експорт | Figma / Ручний експорт | 6 фреймів у Figma | Експорт скріншотів екранів у формат PNG (2x) → збережено у `04_design/screenshots/` | Прийнято; 6 читабельних PNG збережено для аудиту | — |
| **10** | 2026-10-23 / Ходус Данило / G6 | ChatGPT Free / GPT-4o (аналіз зображень) | 6 PNG + `05_Figma_Brief_v1.0.md` | Промпт G6 (текст нижче) → `04_design/06_Review_Report.md` | Проведено підсумковий візуальний аудит екранів; виявлено DEF-10..16 та UX-зауваження | Добовий ліміт завантаження медіа ChatGPT Free; аудит проведено за 6 ключовими PNG |
| **11** | 2026-10-23 / Вдовенко Олег / T-01…T-10 | Figma Present (вручну, без AI) | Клікабельний прототип у Figma | Ручне проходження тест-кейсів T-01..T-10 у режимі презентації Figma | Пройдено 10 ручних тестів; результати зафіксовано в `Test_Cases_T01_T10.md` (100% PASS з урахуванням меж симуляції) | — |

---

## 🧑‍💻 Помилки ШІ, виявлені людиною, та прийняті рішення

| Крок | Хто | Що запропонував / зробив ШІ | Що виправила людина |
| :--- | :--- | :--- | :--- |
| G1 | Вдовенко Олег | ChatGPT включив до MVP US-09 (прикріплення файлів), орієнтуючись на Candidate MVP §4 | Ручний Контроль A за §8: US-09 — Deferred. Зафіксовано рівно 8 US та 33 AC, 100% покриття |
| G2 | Бєлікова Марина | Окрема сторінка для зміни priority, окрема сторінка comments, окремий екран призначення | Відхилено. Усі дії об'єднано в контекстний екран S-03; список — один екран S-02 зі станами All / Important / Empty |
| G4 | Кузнецов Герман | 9 дефектів плану, зокрема повноцінна форма логіна з паролем на S-01 (DEF-08), хоча механізм автентифікації — відкрите питання Q-07 | S-01 залишено умовним плейсхолдером межі доступу (D-02). Затверджено 8 рішень D-01..D-08 зі статусом APPROVED |
| F1/F2 | Салтикова Юлія | Figma Agent намалював порожні квадратні рамки біля заголовків екранів (схожі на чекбокси) та розмістив службові примітки рецензента всередині UI | Рамки видалено вручну; примітки винесено у службовий блок REF-01; Auto Layout за 8-px сіткою; бекап `BEFORE_REVIEW.fig` |
| P1 | Ходус Данило | Figma Agent на безкоштовному тарифі не будує інтерактивні зв'язки | 7 навігаційних маршрутів (таби, overlay модалки, перехід до деталей, повернення) з'єднано вручну |
| G6 | Ходус Данило | ChatGPT виявив DEF-10..DEF-16 та UX-зауваження | Контроль D: некритичне — MITIGATED, незначні розбіжності — ACCEPTED як межі MVP |

## 📝 Повні тексти офіційних запитів (Промптів) до AI

### 1. Промпт G1 — Відбір вимог та створення Input Pack
* **Оператор:** Вдовенко Олег  
* **Інструмент:** ChatGPT Free (GPT-4o)  
* **Контекст:** `SD_Spec.docx` (§0–§8)  
* **Результат:** `01_requirements/01_Input_Pack_v1.0.md`

```text
Ти — аналітик вимог. Створи UX/UI Design Input Pack лише з прикріпленої актуальної специфікації Mini Issue Tracker. Екрани ще не проєктуй.
Спочатку назви прочитаний файл та підтвердь, які його розділи доступні. Якщо матеріал неповний, не роби вигляд, що прочитано все.
Визнач Release MVP за остаточним Release Scope, а не за Candidate MVP. Не трактуй пізніший розділ як автоматичне скасування суперечливих бізнес-правил: суперечності винеси окремо.
Сформуй:
1. Product purpose — до 3 речень; actors та межі першого релізу.
2. Included US; Deferred; Future; explicitly out of scope.
3. Для кожної включеної US — ID, actor, мета, усі AC зі збереженням змісту та вихідних ідентифікаторів.
4. UI-релевантні BR: права, початкові значення, переходи, Important Issues, comments, заборонені дії.
5. Relevant NFR; окремо вимоги, які не перевіряються макетом.
6. Q-ID: конфлікти, прогалини та питання, що потребують рішення людини.
Для кожного твердження вкажи Source: розділ + US/AC/BR або точний пункт. Познач тип: SOURCE / DERIVED / PROPOSED / UNRESOLVED. Висновки DERIVED обґрунтуй джерелами; PROPOSED не включай до обов’язкових вимог.
Не додавай нові функції, поля, ролі, екрани, способи автентифікації чи механізми збереження. Не перетворюй припущення на погоджені рішення. Не вигадуй ID для ненумерованих вихідних критеріїв.
Збережи всі негативні умови: відсутні права, недопустимі переходи, помилка збереження comment, виключення з Important Issues. Розрізняй Not Set як відсутність priority і встановлений рівень priority. Не прирівнюй Resolved до Closed.
Закінчи Source Check: кожна included US → усі її AC → місце у Pack; перелік excluded вимог із причиною; список unresolved питань. Не оголошуй Pack погодженим. Виведи текст, придатний до копіювання в документ.
```

---

### 2. Промпт G2 — Проєктування архітектури поверхонь (Screen Map)
* **Оператор:** Бєлікова Марина  
* **Інструмент:** ChatGPT Free (GPT-4o)  
* **Контекст:** `01_Input_Pack_v1.0.md` + `Decision_Log.md`  
* **Результат:** `02_architecture/02_Screen_Map.md`

```text
Ти — UX architect. Використовуй останній погоджений Input Pack і Decision Log. Не відновлюй Deferred/Future функції з ранньої історії чату.
Побудуй мінімальну систему екранів для Release MVP. Одна User Story не означає один screen: related controls можна розмістити у спільних деталях issue.
Для кожної surface/state запиши:
Screen/State ID | Name | Purpose | Actors | Entry | Visible data | Inputs | Actions | Role/state conditions | Errors/empty states | Exit | Source/D-ID.
Розрізняй screen, state того самого screen, modal/overlay, component state та службову annotation. Визнач також, скільки Figma frames потрібно для демонстрації, не плутаючи це з кількістю продуктових екранів.
Для погодженого варіанта використай: S-01 Authentication boundary; S-02 Issues List зі станами S-02-A All, S-02-B Important, S-02-C Empty; M-01 Create modal; S-03 Issue Details. Не додавати самостійні сторінки Assignment, Priority, Status або Comments.
Зроби таблицю переходів:
T-ID | From | Actor | Trigger | Preconditions | To | Visible result | Requirement/D-ID.
Покрий сценарії: створення та перегляд issue; призначення і priority для Team Lead; дозволені статусні переходи; повернення Resolved у роботу; comment success/error; перегляд Important; заборонена дія для неуповноваженого користувача; порожній список.
Врахуй повернення на попередній list state, якщо це погоджено. Недопустима дія не створює перехід. S-01 залишається placeholder, а не вигаданим login screen.
Дай текстовий user flow для кожного сценарію з ID екранів та очікуваними станами. Наведи 3 приклади того, що НЕ слід додавати, навіть якщо це типово для issue trackers.
Наприкінці: мінімальний Screen Inventory; unresolved рішення; критерії, які план ще не покриває. Не створюй зображення, код чи Figma-файл. Не оголошуй свій план затвердженим.
```

---

### 3. Промпт G3 — Формалізація контрактів екранів для розробника
* **Оператор:** Бєлікова Марина  
* **Інструмент:** ChatGPT Free (GPT-4o)  
* **Контекст:** `Input Pack v1.0`, `Decision Log`, `Screen Map`  
* **Результат:** `02_architecture/03_Screen_Contracts.md`

```text
Підготуй Developer-Verifiable Screen Contracts за погодженим планом. Не додавай продуктових вимог. Нові UX-рішення познач PROPOSED D-ID, а не SOURCE.
Для кожного screen/state запиши:
1. ID, призначення, actors, entry conditions.
2. Visible data: назва поля, обов’язковість, вигляд відсутнього значення.
3. Controls: C-ID, label, type, visible/enabled conditions, trigger, результат, Source/D-ID.
4. Default, empty, validation та error states.
5. Incoming/outgoing transitions з T-ID.
6. Що саме перевіряється в макеті, у прототипі та лише в реалізації.
Окремо сформуй permission matrix для Team Member non-assignee; Team Member assignee; Team Lead non-assignee; Team Lead assignee. Дії: view, create, comment, assign, change priority, change status. Assignee — відношення користувача до issue, не нова глобальна роль. Team Lead не отримує автоматично права на status.
Побудуй повну матрицю status transitions. Поточний status — не новий перехід; Closed не має вихідних переходів. Дозволені лише переходи BR-08.1.
Запиши Important predicate точно: priority у {High, Critical} AND status != Closed. Додай приклади High+Resolved, Critical+Closed та відсутній priority.
Для Create відокрем користувацькі поля від автоматично заданих. Для priority розрізни відсутнє значення та доступні для встановлення значення. Для comments збережи author, time і невдале збереження без створеного comment.
Зроби Traceability:
Source ID/пункт | UIR-ID | Screen/State | C-ID або annotation | Test ID | Verification level.
Покрий усі AC включених US. Для US-03 зберігай посилання на вихідні ненумеровані пункти.
Для кожного тесту: actor/context, precondition, action, expected visible result, що не можна довести цим тестом. Не став PASS за майбутній макет. Перелік потрібних бізнес-рішень виведи окремо.
```

---

### 4. Промпт G4 — Критичний аудит та перевірка плану
* **Оператор:** Кузнецов Герман  
* **Інструмент:** ChatGPT Free (GPT-4o, режим критичного рецензента)  
* **Контекст:** `SD_Spec.docx`, `Input Pack`, `Screen Contracts`, `Traceability`  
* **Результат:** `03_figma_prep/04_Plan_Review.md`

```text
Перевір план як критичний рецензент. Не захищай попередні відповіді. Зістав вихідну специфікацію, погоджені D-рішення, Input Pack, Screen Contracts і Traceability.
Якщо вихідної специфікації немає у доступному контексті, назви обмеження: не стверджуй, що перевірив відповідність S1.
Пройди кожну included US і кожен AC. Шукай: пропуски; зайві функції; підміну вимог UX-рішеннями; неправильні права; незаконні status transitions; неправильне трактування Resolved або Not Set; неможливі маршрути; невизначені результати дій; дублювання екранів; непотрібні product controls; непокриті empty/error states.
Особливо перевір: Team Lead non-assignee не змінює status; у Create тільки Title/Description; Important включає High/Critical Resolved; Closed не має status transitions; усі джерельні ID реальні; backup/HTTPS не перетворено на екрани.
Вихід 1 — матриця coverage для всіх AC: COVERED / MISSING / AMBIGUOUS із доказом у плані.
Вихід 2 — DEF-ID | severity | source | plan location | проблема | мінімальне виправлення. Відокрем вимоговий дефект від необов’язкової UX-пропозиції.
Вихід 3 — Q-ID, які блокують генерацію, та питання, які можна відкласти.
Вихід 4 — PLAN READY / NOT READY з поясненням. READY — тільки рекомендація; остаточне рішення приймає розробник.
Не додавай «покращення» без виявленої проблеми. Не змінюй джерело. Після виправлень дай перелік змінених пунктів, без повного переписування непорушених розділів.
```

---

### 5. Промпт G5 — Збірка компактного Figma brief
* **Оператор:** Кузнецов Герман  
* **Інструмент:** ChatGPT Free (GPT-4o)  
* **Контекст:** `Input Pack v1.0`, `Screen Contracts`, `Decision Log` (APPROVED)  
* **Результат:** `03_figma_prep/05_Figma_Brief_v1.0.md`

```text
Скомпілюй один self-contained англомовний Figma Design implementation brief з погоджених Screen Contracts. Це не новий UX-дизайн і не переказ усієї специфікації.
Обов’язкові секції: purpose and scope; design constraints; canonical screens/states with exact IDs; required labels/data; controls and permissions; status transitions; Important predicate; required empty/error examples; navigation intent; sample data; exclusions; acceptance checklist.
Кожне правило визнач один раз. Збережи Source/D-ID у коротких посиланнях. Не включай Candidate MVP, історію дискусії, backend design і деталізацію Deferred/Future. Заборонені функції переліч один раз.
Попроси: editable Figma-native layers; reusable local components; Auto Layout де доречно; grayscale low-fidelity; meaningful names; одна робоча сторінка; примітки поза продуктовими frames; жодних page icon placeholders, декоративних квадратів, row-selection або bulk controls.
Створи canonical screens і компактні control/state examples; не вимагай повних сторінок для всіх role × status combinations. У state reference повинні бути всі 4 statuses і всі 4 role/assignee contexts.
Для prototype на цьому кроці лише анотації переходів. Не проси Agent експортувати файли чи реалізувати backend, authentication, conditional logic або перевірку прав у коді.
Усі введені UX-рішення повинні вже мати APPROVED D-ID. Якщо рішення необхідне, але не погоджене, не приховуй його у brief — поверни BLOCKER.
Виведи лише текст файла Markdown, без вступу і без зовнішньої рамки коду. Не урізай важливі правила заради заданої кількості символів: обмеження поля запуску вирішується вкладенням файла.
```

---

### 6. Launcher F1 — Генерація макетів у Figma Agent
* **Оператор:** Салтикова Юлія  
* **Інструмент:** Figma Agent (Starter Beta)  
* **Контекст:** Вкладення файлу `05_Figma_Brief_v1.0.md`  
* **Результат:** Початкові фрейми S-01..S-03, бекап `04_design/BEFORE_REVIEW.fig`

```text
Use the attached 05_Figma_Brief_v1.0.md as the approved design contract for Mini Issue Tracker. It is the only source for this generation.
Create the canonical editable low-fidelity screens and compact state reference defined in the file. Keep its exact screen IDs, fields, permissions, transitions and Important Issues rule. Use native editable Figma layers, grayscale, local reusable components and Auto Layout where practical. Keep annotations outside product frames.
Do not add page icons, square icon placeholders, row-selection controls, bulk actions or unsupported features. Do not create full-screen copies for every role/status combination. Do not build prototype interactions or backend logic.
Read the complete attachment before editing. If it is missing, unreadable or contains a blocking unresolved decision, stop and identify the problem; do not invent a design.
After generation, in this same response report:
Created frames/state references; reused components; requirements not represented; assumptions or limitations. Do not claim that persistence, authentication or server permissions were tested.
```

---

### 7. Launcher F2 — Інтегрована корекція макетів у Figma Agent
* **Оператор:** Салтикова Юлія  
* **Інструмент:** Figma Agent / ручна корекція  
* **Контекст:** Виділені робочі фрейми у Figma + бриф  
* **Результат:** Усунення порожніх квадратних рамок біля заголовків, Review notes винесено за межі екранів у REF-01, Auto Layout за 8-px сіткою

```text
Review and minimally correct the selected Mini Issue Tracker frames against the attached approved brief. Preserve screen IDs, valid layout and existing correct content. Do not regenerate the whole design or add features. Edit selected working frames and their local master components only; do not alter backup copies or unrelated pages.
Check: required fields; Create inputs only Title/Description; new issue Open with no priority; approved assignee default; Team Lead-only assignment and priority; current-assignee-only status even for Team Lead; the four allowed transitions; Closed has no outgoing transition; High/Critical Resolved stays Important; Closed and unset/Low/Normal priority are excluded; comments show author/time; empty/validation/save-error examples are present; prohibited features and page icon placeholders are absent; editable layers and consistent components.
Check all four status examples, including In Progress, and all four role/assignee contexts. Separate reviewer annotations from product UI. Do not wire a prototype or claim backend verification.
Fix only evidence-backed noncompliance. If the brief is unavailable or conflicting, stop and name the blocker.
After all edits, provide IN THIS RESPONSE a concise change table:
CHANGE-ID | Screen/layer | What changed | Why | Source rule.
Then list NOT REPRESENTED, UNRESOLVED and anything outside static-design verification. Report actual edits, not intended edits. Do not perform further redesign after the report.
```

---

### 8. Промпт G6 — Фінальний візуальний аудит доказів
* **Оператор:** Ходус Данило  
* **Інструмент:** ChatGPT Free (GPT-4o, аналіз зображень)  
* **Контекст:** 6 скріншотів екранів (`04_design/screenshots/`) + `05_Figma_Brief_v1.0.md`  
* **Результат:** `04_design/06_Review_Report.md` (Контроль D)

```text
Перевір Mini Issue Tracker за погодженими вимогами і наданими доказами. Не вважай звіт Figma Agent доказом виконаної правки.
Спочатку переліч видимі Screen/State IDs і скажи, чи читається текст. Якщо частини нечіткі або відсутні, назви їх. Не реконструюй екран із попереднього prompt.
Частина A — вимоги. Для кожного included AC та UI-релевантного BR/D-рішення заповни:
Source | Expected | Screen/State | Observed evidence | Result | Remaining test.
Results: PASS — очікуваний UI-доказ видно; PARTIAL — видно лише частину; FAIL — видно суперечність; NOT VERIFIABLE — даних недостатньо або потрібна реалізація. Якщо обов'язковий state відсутній у повному заявленому комплекті, це дефект комплекту. Якщо надано лише частину export, не плутай це з доведеною відсутністю state у файлі.
Окремо перевір права, current assignee, початкові значення, усі чотири переходи, Resolved != Closed, Important predicate, comments, validation/empty states та відсутність зайвих функцій і page icon placeholders.
Статичний disabled control не доводить серверну авторизацію; намальований comment не доводить persistence. HTTPS, backup, actual response time і login не позначати PASS за картинкою. Ручні результати прототипу позначати як повідомлення студента, якщо не спостерігаєш їх сам.
Частина B — UX. Дай до 5 доказових проблем навігації, читабельності, зрозумілості дій, consistency, error prevention або базової доступності. Не прирівнюй цей огляд до сертифікації accessibility чи тесту з реальними користувачами.
Частина C — DEF-ID/UX-ID | Severity | Location | Source | Evidence | Minimal correction. Не пропонуй нові функції.
Завершення: 1) UI design coverage — complete/partial/failed; 2) prototype evidence — verified/reported/not provided; 3) implementation tests outstanding. Не давай загального «всі AC виконано», якщо є NOT VERIFIABLE. Не виправляй макет; підготуй перелік для людини.
```
