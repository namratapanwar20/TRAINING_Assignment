**3. Fetch the order id and contact mech id for the shipping address of the orders completed in October of 2023.**<br>

```sql
select 
  oh.order_id, 
  ocm.contact_mech_id 
from 
  order_header oh 
  join order_contact_mech ocm on oh.order_id = ocm.order_id 
  join order_status os on oh.order_id = os.order_id 
  and oh.status_id = os.status_id 
where 
  oh.status_id = ’ORDER_COMPLETED’ 
  and Month(os.status_datetime)= 10 
  and Year(os.status_datetime)= 2023 
  and ocm.contact_mech_purpose_type_id = “SHIPPING_LOCATION”;

```
