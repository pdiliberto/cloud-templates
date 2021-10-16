# Deploying the BIG-IP VE in Google Cloud - HA Cluster (Active/Standby): Existing Stack with BYOL Licensing with a Proxy


I modified the original supported template by F5 (https://github.com/F5Networks/f5-google-gdm-templates/tree/main/supported/failover/same-net/via-api/2nic/existing-stack/byol), to solve deployment issues in isolated VPC.

Those VPCs doesn't have a route to Internet, that is required in a Cloud deployment for many reasons.

In the deployment phase Internet access is required to:
* download BIG-IP Cloud Libs, AS3 and CFE
* BYOL license activation: instances needs connectivity to F5 License Server.

This template allows to use an Internet proxy (that should be already configured and reachable by the VPCs) during the deployment phase, so the instances could download required files and activate themselves even without direct Internet connection.

After the deployment, Active/Standby deployments via API, use CFE (Cloud Failover Extension) to handle correct failover, and it needs to access Storage APIs for shared-state persistence, and to Compute APIs to updates to network resources. These resources are public by default.

If the BIG-IP is deployed without functioning routes to the internet, CFE cannot function as expected.
Please have a look to Matthew Emes' article on DevCentral to configure Google Private Access that solve this issue: https://devcentral.f5.com/s/articles/Installing-and-running-iControl-extensions-in-isolated-GCP-VPCs

If you don't need license activation, (e.g. you are using PAYG), please have a look to Gert Wolfis solution to download required files from a GCP Bucket, so Internet access won't be needed anymore: https://github.com/gwolfis/cloud-solution-templates/tree/master/GCP/bigip-isolated-gdm-usecase


## Deploy the template

This template has exactly the requirements and paramater of the original template, so you would like to have a look to https://github.com/F5Networks/f5-google-gdm-templates/tree/main/supported/failover/same-net/via-api/3nic/existing-stack/byol#deploying-the-template

## Specific Parameters on the YAML file

This template has specifi parameters for Internet proxy:


Parameter | Required | Description
--- | --- | ---
proxyAddr | No | Enter the Internet Proxy IP or hostname, for example, 10.1.2.3.
proxyPort | No | Enter the Internet Proxy Port, for example 3128.
proxyProtocol | No | Enter the proxy protocol: http or https.







