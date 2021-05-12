---
hide:
    - navigation
    - toc
---
# Home

Visualize your Pi-hole in Splunk! If you've landed on this app, it's probably because you are running your own super awesome Pi-hole® server. If not, check it out! [https://pi-hole.net/](https://pi-hole.net/)

This app works with the [Pihole DNS Add-on](https://splunkbase.splunk.com/app/4505/) add-on which provides the field extractions necessary for this app.

This Splunk Add-on is community driven and not affiliated with the official [Pi-hole®](https://pi-hole.net) application. As such, the included documentation does not contain information on how to get started with the Pi-hole DNS server. Rather, this docuemtnation serves as a guide to help visualize the data in Splunk. Please visit [https://pi-hole.net](https://pi-hole.net) for documentation on installing/configuring your own Pi-hole server.

## Key Features

* Allows for easier troubleshooting of blocked queires.
* Prebuilt dashboards that allows you to drilldown to specific queries for further analysis.
* View daily trends and easily identify if querires are outside the month's norm. 
* Test Regex filters before applying them on the Pi-hole server.
* View a list of all DHCP clients.
* Identify errors that may be a result of a misconfiguration.
* Check the DNS queries accross all Pi-hole instances in a single place.
* View Allow and Deny filters setup accross all Pi-hole servers.
* and more!

## Assumptions

This documentation assumes the following:

1. You have a working Pi-hole server.
2. You have a working Splunk environment.
3. Basic understanding of Splunk and Pi-hole.
4. The [Pihole DNS Add-on for Splunk](https://splunkbase.splunk.com/app/4505) has been installed and configured. see [https://splunk-pihole-ta-documentation.rtfd.io/](https://splunk-pihole-ta-documentation.rtfd.io/) for full documentation.

## About

Info | Description
---- | -----------
Version | 2.1.9 - [Splunkbase](https://splunkbase.splunk.com/app/4506) \| [GitHub](https://github.com/ZachChristensen28/pihole_dns_app)
Vendor Product Version | [Pi-hole® v5.3.x, FTL 5.8.x](https://pi-hole.net/)
Add-on has a web UI | Yes, this app contains a collection of dashboards.

[Get Started](getting-started/where-to-install.md){ .md-button .md-button--primary }