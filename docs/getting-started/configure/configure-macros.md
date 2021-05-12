# Update Search Macros

!!! info "Recommended Step"

To ensure this App functions efficiently, it is important to update a few search macros. Change the following macros to their appropriate values.

Macro | Default | Description
----- | ------- | -----------
pihole_index | index=* | Update to the specific index being used for the "pihole" sourcetype.
pihole_dhcp_index | \`pihole_index\` | Update to the specific index being used for the "pihole:dhcp" sourcetype, if different from the main pihole index.
pihole_dhcp_lease_retention | 1209600 <small>(2 weeks)</small> | Default retention time (in seconds) for DHCP hosts. Update as needed.
pihole_blocklist_index | \`pihole_index\` | Update to the index set in the scripted input from the Pihole DNS Add-on.
pihole_summariesonly | summariesonly=false | Defaults to not using summarized data from the CIM. Set to "true" if using data model acceleration.
pihole_system_index | \`pihole_index\` | Update to the specific index being used for the "pihole:system" sourcetype created from the system summary events modular input. see [Pihole Add-on: Modular Inputs](https://splunk-pihole-ta-documentation.rtfd.io/en/latest/getting-started/configure-inputs/configure-modinput/).
pihole_filter_index | \`pihole_index\` | Update to the specific index being used for the pihole:filters sourcetype created from the filters modular input. see [Pihole Add-on: Modular Inputs](https://splunk-pihole-ta-documentation.rtfd.io/en/latest/getting-started/configure-inputs/configure-modinput/).

1. Open the Pihole DNS app for Splunk.
1. Navigate to Settings > Advanced Search > Search macros.

    ??? question "Not seeing any results"
        If no results are found, be sure that the "App" context is set to the Pihole DNS app, owner is set to "Any", and choose "Created in the App" from the remaining drop-down.

1. Update the search macros as necessary.