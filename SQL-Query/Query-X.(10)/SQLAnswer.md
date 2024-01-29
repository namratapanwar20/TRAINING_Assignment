**10.Fetch all the order items that are in the created status and the order type should be a sales order<br>
ORDER_ID<br>
PRODUCT_TYPE_ID<br>
ORDER_LINE_ID<br>
EXTERNAL_ID<br>
SALES_CHANNEL<br>
QUANTITY<br>
ITEM_STATUS <br>
PRODUCT_ID<br>
BILL_CITY<br>
BILL_COUNTRY<br>
BILL_POSTALCODE<br>
BILL_ADDRESS1<br>
BILL_ADDRESS2<br>
SHIP_CITY<br>
SHIP_COUNTRY<br>
SHIP_POSTALCODE<br>
SHIP_ADDRESS1<br>
SHIP_ADDRESS2**

```sql
select 
  oi.order_id, 
  oi.order_item_seq_id as order_line_id, 
  p.product_type_id, 
  oi.external_id, 
  oh.sales_channel_enum_id, 
  oi.quantity, 
  os.status_id, 
  oi.product_id, 
  pa1.address1 as BILL_ADDRESS1, 
  pa1.address2 as BILL_ADDRESS2, 
  pa1.country_geo_id as BILL_COUNTRY, 
  pa1.city as BILL_CITY, 
  pa1.postal_code as BILL_POSTALCODE, 
  pa2.address1 as SHIP_ADDRESS1, 
  pa1.address2 as SHIP_ADDRESS2, 
  pa1.country_geo_id as SHIP_COUNTRY, 
  pa1.city as SHIP_CITY, 
  pa1.postal_code as SHIP_POSTALCODE 
from 
  order_header oh 
  join order_item oi on oi.order_id = oh.order_id 
  join order_contact_mech ocm on ocm.order_id = oh.order_id 
  and ocm.contact_mech_purpose_type_id in (
    "SHIPPING_LOCATION", "BILLING_LOCATION"
  ) 
  left join postal_address pa2 on pa2.contact_mech_id = ocm.contact_mech_id 
  and ocm.contact_mech_purpose_type_id = "SHIPPING_LOCATION" 
  left join postal_address pa1 on pa1.contact_mech_id = ocm.contact_mech_id 
  and ocm.contact_mech_purpose_type_id = "BILLING_LOCATION" 
  join product p on p.product_id = oi.product_id 
  join order_status os on oi.order_id = os.order_id 
  and oi.status_id = os.status_id 
  and oi.order_item_seq_id = os.order_item_seq_id 
where 
  oi.status_id = "ITEM_CREATED" 
  and oh.order_type_id = "SALES_ORDER";

```
