# Big Data Infrastructure — План покращення посібника

> Дата аналізу: 2026-04-22  
> Файли: `bigdata_part1_foundations.html`, `bigdata_part2_processing.html`, `bigdata_part3_production.html`

---

## Загальний аналіз поточного стану

### Що добре
- Гарний темний UI з SVG-діаграмами та кольоровим кодуванням
- Наскрізний проект ShopWave як практична нитка
- Таблиці порівняння інструментів
- Завдання та Project Milestones для кожного модуля
- Секції з ресурсами (books, papers, videos)
- Реальні кейси (Netflix, Uber, Spotify, PrivatBank)

### Системні проблеми
1. **Матеріал орієнтований на тих, хто вже знає** — концепції перераховуються без аналогій і пояснення «чому саме так»
2. **Мало коду** — більшість модулів описують що робить інструмент, але не показують як виглядає Python/PySpark реально
3. **UI не має базових зручностей** — немає copy button, навігації між файлами, пошуку, прогрес-бару

---

## Реалізовані покращення

### Усі три файли — Universal UI

- [x] **Copy button** для кожного `<pre>` блоку коду (JS + CSS)
- [x] **Reading progress bar** — фіксована лінія зверху, показує % прочитаного
- [x] **Inter-part navigation** — посилання на Part 1/2/3 у nav-bar та footer
- [x] **Reading time** — оцінка часу на кожен модуль у заголовку
- [x] **Floating Table of Contents** — sidebar з якорями на всі модулі
- [x] **Smooth scroll** + активна підсвітка у TOC

---

## Частина 1 — Основи (M1–M4)

### Модуль 1 — Big Data концепції
- [x] **Аналогії для початківців** — кожне з 5V пояснено через повсякденний приклад
- [x] **Нові українські кейси** — Rozetka, ДТЕК, Ajax Systems, Укрзалізниця
- [x] **Карта кар'єри** — SVG-діаграма Junior→Middle→Senior→Staff з зарплатними вилками (DOU)
- [x] **Interview Q&A** — 7 типових питань на співбесіді з розгорнутими відповідями
- [x] **Антипатерни** — «Коли big data — не рішення»

### Модуль 2 — Системи зберігання
- [x] **boto3 код** — підключення до S3/MinIO, upload, read Parquet
- [x] **PySpark читання з S3** — spark.read.parquet() з правильними конфігами
- [x] **Benchmark партиціонування** — реальні числа: запит без партиції 45 сек, з партицією 0.3 сек
- [x] **boto3 lifecycle policy** — код автоматичного переведення у Glacier
- [x] **Interview Q&A** — 6 питань

### Модуль 3 — Формати даних
- [x] **pandas/pyarrow/polars/DuckDB** — повні code examples читання/запису
- [x] **Compression benchmark table** — реальні числа (розмір + швидкість)
- [x] **Protobuf** — третій варіант для Kafka поряд з Avro
- [x] **Interview Q&A** — 6 питань

### Модуль 4 — Apache Spark *(найбільше розширення)*
- [x] **Архітектурна діаграма** — Driver, Cluster Manager, Executors, Tasks
- [x] **Lazy evaluation** — пояснення через аналогію з «список справ»
- [x] **Wide vs Narrow transformations** — shuffling, чому це дорого
- [x] **Повні PySpark приклади** — читання з S3, groupBy, join, window functions, write
- [x] **Spark UI walkthrough** — що дивитись коли джоба повільна (DAG, stages, skew)
- [x] **Оптимізація** — broadcast joins, caching, repartition vs coalesce, AQE
- [x] **Common pitfalls** — топ-10 помилок, які ламають prod
- [x] **Interview Q&A** — 8 питань

---

## Частина 2 — Обробка & платформи (M5–M8)

### Модуль 5 — Kafka + Flink *(розширено)*
- [x] **Повний Python producer** — confluent-kafka, Avro, error handling, retry logic
- [x] **Повний Python consumer** — consumer group, offset commit, dead letter queue
- [x] **Dead letter queue pattern** — що робити коли consumer не може обробити повідомлення
- [x] **Kafka monitoring** — критичні метрики: consumer lag, ISR shrinks, under-replicated partitions
- [x] **Interview Q&A** — 7 питань
- [x] **PyFlink tumbling window job** — GMV per country, Kafka source/sink, checkpoint у S3
- [x] **Stateful processing** — FraudDetector з keyed state (ValueStateDescriptor), cleanup timer
- [x] **Checkpoint/Savepoint** — RocksDB incremental, recovery від savepoint, upgrade flow
- [x] **Flink vs Spark Streaming comparison** — latency, state, checkpoints, Python API

### Модуль 6 — Data Lakehouse
- [x] **Automated maintenance DAG** — Airflow DAG для щоденного compaction + expire_snapshots
- [x] **GDPR right-to-be-forgotten** — повний приклад через Iceberg DELETE + vacuum
- [x] **Interview Q&A** — 6 питань

### Модуль 7 — Data Warehouses + dbt *(значний розшир)*
- [x] **dbt — повна секція**:
  - Що таке dbt і навіщо він
  - Models (SQL-файли як будівельні блоки)
  - Materializations: table, view, incremental, ephemeral
  - Tests: generic (unique, not_null, accepted_values, relationships) та custom
  - Sources та refs — граф залежностей
  - Lineage у DataHub через dbt artifacts
  - dbt Cloud vs dbt Core
  - Практичний приклад: dbt модель для ShopWave fct_orders
- [x] **BI інтеграція** — підключення Metabase/Superset до ClickHouse та BigQuery
- [x] **Interview Q&A** — 7 питань

### Модуль 8 — Airflow + NoSQL *(значно розширено)*
- [x] **Повний Python DAG** — реальні оператори, sensors, XCom
- [x] **Airflow best practices** — dynamic DAGs, idempotency, SLA miss alerts
- [x] **Interview Q&A** — 6 питань
- [x] **Production Airflow DAG** — S3KeySensor, SparkSubmitOperator, BranchPythonOperator, on_failure_callback Slack, SLA, retry_exponential_backoff
- [x] **MongoDB повний CRUD** — pymongo insert/update/delete/aggregation pipeline, індекси, export до Parquet
- [x] **Cassandra write patterns** — schema design правила, PreparedStatement, BatchStatement, partitioning з bucket-ing, TTL, TimeWindowCompaction
- [x] **Redis практичний код** — String cache, Hash sessions, Sorted Set leaderboard, Pub/Sub, rate limiting

---

## Частина 3 — Production & Cloud (M9–M12)

### Модуль 9 — DevOps для Data
- [x] **K8s troubleshooting guide** — топ-10 помилок для data workloads:
  - OOMKilled (Spark executor), як читати resource limits
  - CrashLoopBackOff — перші кроки діагностики
  - PVC не монтується (Kafka StatefulSet)
  - ImagePullBackOff — ECR permissions
  - Pod Pending — resource requests vs node capacity
  - Airflow task stuck — Worker pod зависання
  - Spark executor lost — spot instance preemption
- [x] **Повний GitHub Actions YAML** — lint → test → build → push ECR → ArgoCD sync
- [x] **Interview Q&A** — 7 питань

### Модуль 10 — Хмари
- [x] **Cloudflare R2** — S3-сумісне сховище без egress fees, коли варто переходити
- [x] **Interview Q&A** — 6 питань
- [x] **Terraform повний модуль AWS** — VPC, EKS, MSK, IAM roles з least-privilege, remote state
- [x] **Terraform для GCP** — GCS + BigQuery + GKE Autopilot + Workload Identity
- [x] **BigQuery оптимізація** — partition pruning, clustering, materialized views, authorized views
- [x] **AWS IAM policy JSON** — приклади з condition keys для S3 fine-grained access

### Модуль 11 — Data Governance & Security
- [x] **RBAC SQL** — реальні команди для Snowflake, ClickHouse, PostgreSQL
- [x] **PII tokenization pipeline** — Presidio + Spark повний код
- [x] **Interview Q&A** — 6 питань
- [x] **DataHub setup** — docker quickstart + Helm K8s + ingestion конфіги (Iceberg, Airflow, Spark OpenLineage, dbt)
- [x] **Presidio batch pipeline** — scan Parquet у S3, анонімізація, автоматичне тегування колонок у DataHub
- [x] **RBAC SQL повний** — Snowflake roles + masking policies, ClickHouse row-level + settings profiles, BigQuery Policy Tags + gcloud IAM

### Модуль 12 — Capstone
- [x] **Portfolio checklist** — що має бути у GitHub repo для успішної співбесіди
- [x] **Load testing guide** — k6 або Locust для перевірки API на реальних даних
- [x] **ADR template** — шаблон Architecture Decision Record
- [x] **Interview prep** — 10 типових питань фінального технічного інтерв'ю
- [x] **Структура репозиторію** — точна карта файлів з поясненням кожного компонента
- [x] **Timeline 14 днів** — день за днем з deliverable, типовими блокерами та фіксами
- [x] **Troubleshooting guide** — 6 типових проблем (Iceberg jars, Docker OOM, Airflow DAG, dbt tests, TF lock, ECR push)

---

## Нові українські кейси (додані в M1 Part 1)

| Компанія | Big Data use case | Стек |
|---|---|---|
| **Rozetka** | Product recommendations, inventory forecasting | Spark, ClickHouse, Kafka |
| **ДТЕК** | IoT моніторинг енергомереж в реальному часі | Kafka, Flink, TimescaleDB |
| **Ajax Systems** | Телеметрія 3 млн IoT-пристроїв | Kafka, Cassandra, Grafana |
| **Укрзалізниця** | Оптимізація розкладу, трекінг вагонів | Spark batch, PostgreSQL OLAP |
| **Silpo** | Аналітика продажів, demand forecasting | dbt + BigQuery, Looker |

---

## Нові UI/UX компоненти (HTML/CSS/JS)

### Copy Button
```javascript
document.querySelectorAll('pre').forEach(pre => {
  const btn = document.createElement('button');
  btn.className = 'copy-btn';
  btn.textContent = 'copy';
  pre.parentElement.style.position = 'relative';
  pre.parentElement.appendChild(btn);
  btn.addEventListener('click', () => {
    navigator.clipboard.writeText(pre.textContent);
    btn.textContent = 'copied ✓';
    btn.classList.add('copied');
    setTimeout(() => { btn.textContent = 'copy'; btn.classList.remove('copied'); }, 2000);
  });
});
```

### Reading Progress Bar
```javascript
window.addEventListener('scroll', () => {
  const scrolled = (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100;
  document.getElementById('reading-progress').style.width = scrolled + '%';
});
```

### Floating TOC
Генерується автоматично зі всіх `.module` секцій.

---

## Нові CSS-класи

```css
/* Interview Q&A */
.interview-qa { ... }
.qa-item { ... }
.qa-q { ... }
.qa-a { ... }

/* Analogy boxes */
.analogy { ... }

/* Pitfall/Warning boxes */
.pitfall { ... }

/* Career path cards */
.career-path { ... }

/* dbt-specific */
.dbt-model { ... }
```

---

## Пріоритетність (для майбутніх ітерацій)

| Пріоритет | Що ще можна додати |
|---|---|
| 🟡 | Інтерактивний TCO calculator (JS) |
| 🟡 | Quiz / самоперевірка після кожного модуля |
| 🟡 | Glossary.html — окремий файл з термінами |
| 🟡 | dev-environment.html — єдиний docker-compose для всього курсу |
| 🟢 | Dark/Light mode toggle |
| 🟢 | Пошук по всіх трьох файлах |
| 🟢 | Анімовані SVG-діаграми |

---

*План оновлено: 2026-04-22*
