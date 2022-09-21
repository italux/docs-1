# \[Azure] Kubecost Asset Audit

**\[Azure]**

The first step of auditing Kubecost data is reconciling asset prices to cloud provider data. Before doing this step, we recommend completing a cloud provider integration for higher accuracy. [Learn more about why](https://github.com/kubecost/docs/blob/master/assets.md#cloud-cost-reconciliation)

| Note: it’s recommended that you select a time window where Kubecost was collecting data.48 hours in the past, because cloud provider data can be delayed up to 2 days. |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Step 1:** Visit Kubecost Assets page

![](.gitbook/assets/0)

**Step 2:** Target a specific day in date range. Do the same in the Azure billing console. In this example we use September 8th, 2022. Aggregate by Service and be sure to include the appropriate filters, including the appropriate account being audited in the Azure Billing Console. Failure to filter appropriately in Azure’s cost analysis console and Kubecost will result in inaccurate pricing.

**Kubecost console**

![](<.gitbook/assets/1 (3)>)

**Azure Cost Management Console**&#x20;

<figure><img src=".gitbook/assets/2" alt=""><figcaption></figcaption></figure>



Step 3: Repeat the process for other Azure resources. Most other resources will be 1:1 matching.
