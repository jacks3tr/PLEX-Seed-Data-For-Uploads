*The following queries are intended to be used in the TEST database to create data for testing purposes

# PLEX-Smart-Inventory-Upload
This query works in the SQL Development Environment for the PLEX ERP. It will generate a file that will create a container for each part that is currently in the system. By uploading this file in the TEST database you can test all scenarios that your master data permits. 

-	The backup Container is ‘Bin’ you need to have this container type or change it in the select statement
-	The current location is ‘Receiving’ you need to have this location or change it in the select statement
o	If you want dynamic locations, the following would put certain operations in shipping or receiving and everything else at the locations of the workcenters on the routing: Case when o.operation_code like '%fg%' then 'Shipping' when O.operation_code like '%rec%' then 'Receiving' when O.operation_code like '%sub%' then 'Receiving' else w.workcenter_code end as location, 
-	It rounds quantity and weights to whole numbers to avoid regional issues like decimal/comma differences.
-	If you have data that includes leading 0’s, commas, etc. you will need to use XML and may still have issues (I try to avoid data like this).
-	I wrote this in a general way that should work for most projects. However, it doesn’t account for all configs (lot management, for example) – in those cases, it should be useful as a starting point.  

# PLEX-Seed-Data-For-Uploads
The remaining quieries will return a simple list of the currently active parts or routings to be the basis for various uploads to be used in the TEST database. 
