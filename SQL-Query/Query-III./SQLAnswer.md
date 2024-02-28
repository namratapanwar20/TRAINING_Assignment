**3. Average number of shipments per month:**
Monthly

```sql
select
  extract(YEAR_MONTH from STATUS_DATE) as month
  count(SHIPMENT_ID)/ count(
    distinct extract(
      YEAR_MONTH 
      from 
        STATUS_DATE
    )
  ) as AVERAGE 
from 
  shipment_status 
where 
  status_id = 'SHIPMENT_SHIPPED';
```

Yearly

```sql
select extract(year from status_date) as year,
  count(SHIPMENT_ID)/12 as average
from
  shipment_status
where
  status_id = 'SHIPMENT_SHIPPED'
group by
  year;
```
