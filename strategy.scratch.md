

sample of train table
```sql
(SELECT
  *
FROM
  `sertis-test-425103.sales.train`
WHERE
  onpromotion = 'True'
limit 1)

union all

(SELECT
  *
FROM
  `sertis-test-425103.sales.train`
WHERE
  onpromotion = 'False'
limit 1)

union all

(
SELECT
  *
FROM
  `sertis-test-425103.sales.train`
WHERE
  onpromotion is null
limit 2
)
```