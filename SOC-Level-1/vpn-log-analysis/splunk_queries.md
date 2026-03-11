# Splunk Queries Used

## Show all VPN logs

index=VPN_Logs

## Identify login events

index=VPN_Logs action=built

## Count user logins

index=VPN_Logs action=built | stats count by UserName

## Identify VPN activity by state

index=VPN_Logs | stats count by source_state

## Detect repeated connections

index=VPN_Logs action=built | stats count by Source_ip