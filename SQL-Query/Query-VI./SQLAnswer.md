**6. Total $ value of shipments shipped from facility 904/906 to first quarter:**
```sql
select 
  sum(UNIT_PRICE * QUANTITY) TOTALMONETARYVALUE 
from 
  order_item 
where 
  ORDER_ID in (
    select 
      ORDER_ID 
    from 
      order_header 
    where 
      CURRENCY_UOM = 'USD' 
      and ORDER_ID in (
        select 
          ORDER_ID 
        from 
          order_shipment 
        where 
          SHIPMENT_ID in (
            select 
              SHIPMENT_ID 
            from 
              shipment 
            where 
              SHIPMENT_ID in (
                select 
                  SHIPMENT_ID 
                from 
                  shipment_status 
                where 
                  STATUS_ID = 'SHIPMENT_SHIPPED' 
                  and month(STATUS_DATE) in (1, 3) 
                  and year(STATUS_DATE)= 2022
              ) 
              and (
                ORIGIN_FACILITY_ID = '904' 
                OR ORIGIN_FACILITY_ID = '906'
              )
          )
      )
  );
```
