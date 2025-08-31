
###  Portfolio Project 3: Cohort Analysis
Conducted a cohort analysis using **Tableau** to visualize the percentage of subscribers who opened marketing emails after account creation. The dataset for this analysis was sourced from Google **BigQuery**.

### Portfolio-3: Когортний аналіз
Зробив когортний аналіз за допомогою Tableau, який демонструє відсоток підписників, які відкривають електронні листи після створення акаунту. Щоб отримати датасет для аналізу, використав дані з BigQuery.

---

## Purpose of the query
This query calculates accounts and their return activity through email clicks.

## Намір запиту
Цей запит вираховує акаунти та їх повернення в кліки по листу.

'''sql

WITH UserCohorts AS (
  SELECT
    acs.account_id,
    MIN(s.date) AS cohort_date
  FROM
    `DA.account_session` AS acs
  JOIN
    `DA.session` AS s
    ON acs.ga_session_id = s.ga_session_id
  GROUP BY
    acs.account_id
)
SELECT
  uc.account_id,
  uc.cohort_date,
  ev.visit_date AS activity_date
FROM
  UserCohorts AS uc
LEFT JOIN
  `DA.email_visit` AS ev
  ON uc.account_id = ev.id_account
WHERE
  
  ev.visit_date IS NOT NULL
ORDER BY
  uc.account_id,
  activity_date;
'''

---

**Dataset for analysis/[Датасет для аналізу](https://drive.google.com/file/d/1MnecUS4FoGDREN37fd_FCZJkIZ6G66FA/view?usp=sharing)**

---

## Analysis result
Based on this dataset, I created a cohort analysis in Tableau. The X-axis displays the number of weeks that have passed since the account was created, while the Y-axis represents cohorts grouped by the week of account creation.

## Результат аналізу
На основі цього датасету вивожу в Tableau когортний аналіз. На осі Х потрібно відобразити кількість тижнів, що минули з моменту створення акаунта в системі, а на осі Y – когорти, сформовані за тижнями створення акаунтів.

---

**Interactive dashboard in Tableau Public/[Інтерактивний дашборд в Tableau Public](https://public.tableau.com/app/profile/oleksandr.oleksandr7187/viz/_17518209021980/sheet1)**

---

## Conclusions and Recommendations
* **Users churn quickly:** Most newly registered users leave almost immediately and do not return.
* **Weak initial engagement:** Very few users take meaningful action during their first week after registration.
* **The first days are critical:** If users aren’t engaged right away, they are likely to leave for good.

## What to do about it?
* **Welcome new users immediately:** As soon as someone registers, send them a series of helpful emails during their first week.
* **Re-engage dormant users:** If someone hasn’t logged in for 2–3 weeks, send them an email with an enticing offer to encourage them to return.
* **Give users a reason to come back:** Ask yourself—why should someone visit your platform every week?


## Висновки і рекомендації
* **Ядро швидко йдуть:** Більшість тих, хто зареєструвався, майже одразу зникають і більше не повертаються.
* **Початок дуже слабкий:** Майже ніхто нічого не робить у перший тиждень після реєстрації.
* **Найважливіші – перші дні:** Якщо не зацікавити людину відразу, воно, виходячи за все, піде назавжди.

## Що з цим робити?

* **Негайно вітайте нових людей:** Щойно людина зареєструвалася, одразу ж надішліть їй кілька корисних листів протягом першого тижня.
* **Нагадайте про себе тим, хто "заснув":** Якщо людина не заходила 2-3 тижні, надішліть їй лист із цікавою пропозицією, щоб вона захотіла повернутися.
* **Дайте людям причину повертатися:** Подумайте: чому людина має заходити до вас щотижня?

---
