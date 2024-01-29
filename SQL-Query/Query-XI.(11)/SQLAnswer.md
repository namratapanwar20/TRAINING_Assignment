**11.Fetch all the customers in June 2023.**

```sql
select 
  party_id 
from 
  party 
where 
  party_id in (
    select 
      party_id 
    from 
      party_role 
    where 
      role_type_id = "CUSTOMER"
  ) 
  and status_id = "PARTY_ENABLED" 
  and Month(created_date)= 6 
  and Year(created_date)= 2023;

```
