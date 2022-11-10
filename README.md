# \[AWS] Kubecost Asset Audit

The first step of auditing Kubecost data is reconciling asset prices to cloud provider data. Before doing this step, we recommend completing a cloud provider integration for higher accuracy. [Learn more about why](https://github.com/kubecost/docs/blob/master/assets.md#cloud-cost-reconciliation)

**Step 1:** Visit Kubecost Assets page

![](<.gitbook/assets/0 (3)>)

**Step 2:** Select a particular service, e.g. _Kubernetes,_ and then select an asset type, e.g. Kubernetes _nodes_

![](<.gitbook/assets/1 (1)>)

**Step 3a:** Compare hourly prices of individual nodes in the Kubecost UI against cloud provider rates. Each provider’s respective billing rates can be found here:

* [GCP billing rates](https://cloud.google.com/compute/all-pricing)
* [AWS VM rates](https://aws.amazon.com/ec2/pricing/on-demand/)
* [Azure VM rates](https://azure.microsoft.com/en-us/pricing/details/virtual-machines/linux/)

OR

**Step 3b:** Select a specific time window and compare against your actual cloud provider bill.

| Note: it’s recommended that you select a time window where Kubecost was collecting data.48 hours in the past, because cloud provider data can be delayed up to 2 days. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

This process can be repeated for other services & asset types. Below is an example.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>Kubecost</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (2) (1).png" alt=""><figcaption><p>AWS Cost Explorer</p></figcaption></figure>
