**2. Shipment by Tracking number:**
```sql
 select 
  SHIPMENT_ID, TRACKING_ID_NUMBER  
from 
  shipment_route_segment 
where 
  TRACKING_ID_NUMBER is not null;
```
