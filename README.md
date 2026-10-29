# Лабораторна робота 8. RDF-сховище знань «Управління надзвичайними ситуаціями»

Тема: управління надзвичайними ситуаціями (дані EM-DAT за 2023 рік). Тематична область та IRI збігаються з лабораторною 7.

## Файли
| Файл | Призначення |
|---|---|
| vocabulary.ttl | словник (RDFS/OWL): 18 класів, 6 об’єктних і 8 датних властивостей; повторно використано SKOS, Dublin Core Terms, PROV-O (135 триплетів) |
| data.ttl | набір даних (ABox): 145 триплетів |
| context.jsonld | JSON-LD context для того самого набору |
| queries.rq | 6 запитів SPARQL: 4 SELECT, 1 ASK, 1 CONSTRUCT |
| updates.rq | 2 SPARQL UPDATE та контрольні запити «до/після» |
| shapes.ttl | 3 SHACL-шаблони |
| invalid_data.ttl | невалідні приклади для SHACL |
| screenshots/ | скриншоти інтерфейсу сховища |

## Розгортання (GraphDB Free, http://localhost:7200)
1. Створіть репозиторій `emergency_plain` (ruleset: Empty, увімкнути SHACL validation) і `emergency_rdfs` (ruleset: RDFS).
2. У `emergency_plain`: імпортуйте `shapes.ttl` в іменований граф `http://rdf4j.org/schema/rdf4j#SHACLShapeGraph`, потім `vocabulary.ttl` і `data.ttl`.
3. У `emergency_rdfs`: імпортуйте `vocabulary.ttl` і `data.ttl`.
4. Виконайте запити з `queries.rq` і `updates.rq`; спроба імпорту `invalid_data.ttl` у `emergency_plain` має завершитися помилкою валідації.

## Приклад звернення до SPARQL-endpoint
```
curl -G "http://localhost:7200/repositories/emergency_plain" -H "Accept: text/csv" --data-urlencode "query=SELECT ?s WHERE { ?s a <http://example.org/emergency#Країна> }"
```

## Використання ШІ
Чернетки словника, даних, запитів, шаблонів SHACL і звіту підготовлено за допомогою ШІ-асистента Claude (Anthropic); розгортання сховища, виконання запитів і перевірку результатів виконано автором роботи.
