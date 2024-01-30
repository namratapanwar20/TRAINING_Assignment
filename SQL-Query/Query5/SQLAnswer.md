**5. In New York, which product has the highest sales?**

Using Billing Location : 
```sql
select 
  oi.product_id, 
  sum(oi.quantity) as highest_sales 
from 
  order_item oi 
  join order_header oh on oh.order_id = oi.order_id 
  join order_contact_mech ocm on ocm.order_id = oh.order_id 
  join postal_address pa on pa.contact_mech_id = ocm.contact_mech_id 
where 
  oh.order_type_id = "SALES_ORDER" 
  and ocm.contact_mech_purpose_type_id = "BILLING_LOCATION" 
  and pa.city = "NEW YORK" 
group by 
  product_id 
order by 
  sum(oi.quantity) desc 
limit 
  1;
```

Using Shipping Location : 
```sql
select 
  oi.product_id, 
  sum(oi.quantity) as highest_sales 
from 
  order_item oi 
  join order_header oh on oh.order_id = oi.order_id 
  join order_contact_mech ocm on ocm.order_id = oh.order_id 
  join postal_address pa on pa.contact_mech_id = ocm.contact_mech_id 
where 
  oh.order_type_id = "SALES_ORDER" 
  and ocm.contact_mech_purpose_type_id = "SHIPPING_LOCATION" 
  and pa.city = "NEW YORK" 
group by 
  product_id 
order by 
  sum(oi.quantity) desc 
limit 
  1;
```
