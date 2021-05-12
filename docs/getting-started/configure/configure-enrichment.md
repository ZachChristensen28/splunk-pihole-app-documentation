# Configure Enrichment

!!! info "Optional Step"

This app can automatically enrich IPs with hostnames populated from DHCP events. This step can be skipped if enrichment is not required.

The steps to setup enrichment for this app utilize Splunk Lookups. For more information on lookups see [Splunk Docs: About lookups](https://docs.splunk.com/Documentation/Splunk/latest/Knowledge/Aboutlookupsandfieldactions).

## Pi-hole DHCP Enrichment Configuration

!!! note
    The following steps only apply if you are using your Pi-hole server as your DHCP server. If you are not using the Pi-hole as your DHCP server, see [Alternative Enrichment Configuration](#alternative-enrichment-configuration).

For the built-in DHCP hostname enrichment to work, there are two scheduled searches that need to be enabled <small>(Disabled by default)</small>.

Search Name | Description | Default Schedule
----------- | ----------- | ----------------
Pihole - Create DHCP Lease Lookup | Only needs to be run once. This will create the initial lookup for DHCP leases. Defaults to the last 7 days. | None
Pihole - DHCP Leases Lookup - Gen | Recurring search to keep DHCP leases up to date. | Runs Hourly
<small>(Optional)</small> Pihole - DHCP Remove Old Leases | This search will remove leases that have not been updated for a period of time. The default is two weeks. | Once per day

1. From Splunk Web, open the Pihole DNS App for Splunk.
1. Navigate to Settings > Searches, Reports, and Alerts.
1. Ensure the "App" context is the Pihole DNS App for Splunk by using the dropdown.
1. Set the "Owner" to "all"
1. For each Search wanting to be enabled click "Edit" > "Enable"

## Alternative Enrichment Configuration

### Static Lookup File

Using a static lookup file may be the simplest way to get started for enriching IPs with hostnames. The static list takes more to maintain but is easier to get started. If your environment utilizes static IPs or DHCP reservations, this option is the easiest choice.

!!! note
    If you already have a lookup file to map IPs to hostnames, see [Use an existing lookup file](#use-an-existing-lookup-file).

#### Method 1 - Use the Lookup Editor

<small>Recommended</small>

The lookup editor may be the easiest way to create and mange lookups in Splunk. You can download and install the Lookup Editor from [Splunkbase: Lookup Editor](https://splunkbase.splunk.com/app/1724).

Once installed, the lookup editor can be used to create a new CSV lookup.

1. Open the Lookup Editor in Splunk Web.
1. Click "Create a New Lookup" > CSV lookup.
1. Give the lookup a descriptive name.
1. Choose which App context this lookup will be stored in <small>(i.e. Search & Reporting)</small>.
1. Leave the "User-only" box uncheked. This will give the lookup the global scope permissions it needs. 
1. Create column headers (row 1). This app uses the following for the CSV header, however, any field names can be used.

    ```text
    dest_nt_host,dest_ip,dest_mac
    ```

1. Populate the remaing rows with the IP and host information.
1. Once saved, move on to [Update Search Macro](#update-search-macro).

#### Method 2 - Create and Upload a new CSV file

A lookup file can be created outside of Splunk and then uploaded via the web interface.

1. Use an editor to create a file in CSV format.
1. Create column headers (row 1). This app uses the following for the CSV header, however, any field names can be used.

    ```text
    dest_nt_host,dest_ip,dest_mac
    ```

1. Populate the remaing rows with the IP and host information.
1. Be sure to save the file with a `.csv` extension.
1. Open Splunk Web.
1. Navigate to Settings > Lookups > Lookup table files (click "+ Add new")
1. Select the Destination App <small>(i.e. Search & Reporting)</small>.
1. Upload the file.
1. Provide the Destination filename. This can be the same name as the one created <small>(i.e. pihole_lookup.csv)</small>.
1. Once saved, Navigate back to Settings > Lookups > Lookup table files, if you are not already there.
1. Search for the name of the file you just uploaded.
1. Modify the permissions for the file by clicking "Permissions."
1. Select "All apps (system)" from the two radio options.
1. Check "Read" permissions for Everyone. Write permissions can be given as needed (typically set to admin & power).
1. After saving, move to [Update Search Macro](#update-search-macro).

### Use an existing lookup file

If you already have an existing lookup file that contains a mapping of hostnames and IPs, ensure the following:

1. The lookup file has a global scope.
1. Users are able to read the lookup file. 
1. If you are using a lookup file and a lookup definition, also ensure the lookup definition has the same permissions as above.

Once verified the correct permissions are set, see [Update Search Macro](#update-search-macro).

### Update Search Macro

Once you have a lookup file conatined with IP and hostname information, the default search macro must be updated for automatic enrichment.

1. Open the Pihole DNS app for Splunk.
1. Navigate to Settings > Advanced Search > Search macros.

    ??? question "Not seeing any results"
        If no results are found, be sure that the "App" context is set to the Pihole DNS app, owner is set to "Any", and choose "Created in the App" from the remaining drop-down.

1. Click "pihole_enrich_hostname(1)". This opens up the editor page.
1. Modify the fields contained by "< >" with the correct values:

    ```text
    lookup <your_lookup.csv> <your_ip_field> as "$ip_field$" OUTPUTNEW <your_hostname_field> as Hostname
    ```

    ???+ tip "Example"
        ```text
        lookup pihole_lookup.csv client_ip as "$ip_field$" OUTPUTNEW client_name as Hostname
        ```

1. After saving, navigate back to the Pihole DNS app and you should now see the "Hostname" field being populated. If not, see [Troubleshooting Enrichment](../troubleshooting/troubleshoot-enrichment.md).