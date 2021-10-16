# Deploying the BIG-IP VE in Google Cloud - HA Cluster (Active/Standby): Existing Stack with BYOL Licensing with a Proxy

I modified the original supported template by F5 (https://github.com/F5Networks/f5-google-gdm-templates/tree/main/supported/failover/same-net/via-api/3nic/existing-stack/byol), because I have a need to work in an isolated environment.

Internet access is needed to download BIG-IP Cloud Libs, AS3 and CFE.

Being an A/S deployment with API, it utilizes F5 CFE (Cloud Failover Extension), that needs to access Storage APIs for shared-state persistence, and to Compute APIs to updates to network resources. If the BIG-IP is deployed without functioning routes to the internet, CFE cannot function as expected.
Please have a look to Matthew Emes' article on DevCentral to configure Google Private Access that solve this issue: https://devcentral.f5.com/s/articles/Installing-and-running-iControl-extensions-in-isolated-GCP-VPCs

## Deploy the template

This template has exactly the requirements and paramater of the original template, so you would like to have a look to https://github.com/F5Networks/f5-google-gdm-templates/tree/main/supported/failover/same-net/via-api/3nic/existing-stack/byol#deploying-the-template

## Specific Parameters on the YAML file

This template has specifi parameters for Internet proxy:


Parameter | Required | Description
--- | --- | ---
proxyAddr | No | Enter the Internet Proxy IP or hostname, for example, 10.1.2.3.
proxyPort | No | Enter the Internet Proxy Port, for example 3128.
proxyProtocol | No | Enter the proxy protocol: http or https.







