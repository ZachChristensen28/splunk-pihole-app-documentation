# Troubleshoot Enrichment

## Common Problems

### Permission Issue

The most common problem with not seeing hostnames populated is that the permissions for the lookup file are not correct. Check the following.

1. In Splunk Web, Navigate to Settings > Lookups > Lookup table files.
1. Search for the name of your lookup file.
1. Verify the permissions for the file by clicking "Permissions."
1. Be sure "All apps (system)" is selected.
1. Be sure "Read" permissions is granted to Everyone.

If you are utilizing a lookup definition, perform the same steps for the definition.

### Search Macro Definition

Check the search macro `pihole_enrich_hostname(1)` for accuracy. It may be possible that there is a typo in the changed values. Be sure that the `lookup_file`, `host ip`, and `hostname` fields are all correct from the following syntax:

!!! tip ""
    lookup `lookup_file` `host_ip` as "$ip_field$" OUTPUTNEW `hostname` as Hostname

Field | Description
----- | -----------
lookup_file | The name of your lookup <small>(i.e. pihole_lookup.csv).
host_ip | the IP field from your lookup.
hostname | the hostname field from your lookup.