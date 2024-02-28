**6. In the past month, which store has the highest number of one-day shipped orders?**

```sql
select 
  f.facility_name, 
  count(oisg.order_id) as Shipped_orders 
from 
  order_item_ship_group oisg 
  join order_status os on oisg.order_id = os.order_id 
  join facility f on oisg.facility_id = f.facility_id 
  join facility_type ft on f.facility_type_id = ft.facility_type_id 
where 
  os.status_id = 'ORDER_COMPLETED' 
  and os.status_datetime >= DATE_SUB(
    CURDATE(), 
    INTERVAL 1 MONTH
  ) 
  and os.status_datetime < CURDATE() 
  and oisg.shipment_method_type_id = 'NEXT_DAY' 
  and ft.parent_type_id = "PHYSICAL_STORE" 
group by 
  oisg.facility_id 
order by 
  Shipped_orders desc 
limit 
  1;
```
