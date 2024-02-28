**7. On a city-wise basis, what is the analysis of returns?**

```sql
select 
  pa.city, 
  rh.return_id 
from 
  return_header rh 
  join return_contact_mech rcm on rcm.return_id = rh.return_id 
  join postal_address pa on pa.contact_mech_id = rcm.contact_mech_id 
group by 
  pa.city;

```
