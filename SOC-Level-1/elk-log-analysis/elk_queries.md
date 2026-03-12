# ELK Queries Used

## View all logs
*

Displays all log entries in the index.

## Search for VPN login events
action:"built"

Filters events where a VPN connection was successfully established.

## Search for a specific user
UserName:"James"

Returns log events associated with the user James.

## Search for a specific IP address
Source_ip:"157.109.0.102"

Filters logs generated from a specific source IP address.