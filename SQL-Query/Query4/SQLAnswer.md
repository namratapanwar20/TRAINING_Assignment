**4. What is the total number of orders originating from New York?**

```sql
select 
  count(distinct oh.order_id) as total_orders 
from 
  order_header oh 
  join order_contact_mech ocm on ocm.order_id = oh.order_id 
  and ocm.contact_mech_purpose_type_id = "SHIPPING_LOCATION" 
  join postal_address pa on pa.contact_mech_id = ocm.contact_mech_id 
where 
  pa.city = "New York";

```
