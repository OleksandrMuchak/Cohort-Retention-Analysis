
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
   DATE_TRUNC(MIN(s.date), WEEK) AS cohort_week
 FROM
   `DA.account_session` AS acs
 JOIN
   `DA.session` AS s
   ON acs.ga_session_id = s.ga_session_id
 GROUP BY
   acs.account_id
)
SELECT
 uc.cohort_week,
 FLOOR(ev.visit_date / 7) AS week_number_since_registration,
COUNT(DISTINCT uc.account_id) AS active_users
FROM
 UserCohorts AS uc
JOIN
 `DA.email_visit` AS ev
 ON uc.account_id = ev.id_account
WHERE
 ev.visit_date >= 0
GROUP BY
 cohort_week,
 week_number_since_registration
ORDER BY
 cohort_week,
 week_number_since_registration;
'''

---

**Dataset for analysis/[Датасет для аналізу]
(https://drive.google.com/file/d/1BpvsbtUwGb8y5-IRpNQBAl3236z3PQXH/view?usp=sharing)**

---

## Analysis result
Based on this dataset, I created a cohort analysis in Tableau. The X-axis displays the number of weeks that have passed since the account was created, while the Y-axis represents cohorts grouped by the week of account creation.

## Результат аналізу
На основі цього датасету вивожу в Tableau когортний аналіз. На осі Х потрібно відобразити кількість тижнів, що минули з моменту створення акаунта в системі, а на осі Y – когорти, сформовані за тижнями створення акаунтів.

---

**Interactive dashboard in Tableau Public/[Інтерактивний дашборд в Tableau Public](https://public.tableau.com/app/profile/oleksandr.oleksandr7187/viz/WeeklyUserRetentionbyCohort/WeeklyUserRetentionbyCohort)**

---



---
