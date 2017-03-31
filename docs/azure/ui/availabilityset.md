#### Availability sets and rack awareness

*Availability sets*

Azure implements the concept of [“Availability Sets”](https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-linux-manage-availability) to support fault tolerance for VM's. This feature allows two or more VM's to be mapped to multiple fault domains. Fault domains define the group of virtual machines that share a common power source and network switch. VM's with different fault domains are guaranteed an SLA. This SLA includes guarantees that during OS Patching in Azure or during maintenance operations, at least one VM belonging to a different fault domain will be available.

Availability sets have either two or three Fault Domains, each sharing a common power source and network switch. When adding VM-s to an availability set, Azure automatically assigns each VM a Fault Domain.

In Cloudbreak UI, availability sets can be configured during cluster creation. First, you have to enable availability sets with the checkbox under `Configure Cluster` tab. Then you can add the desired availability sets by providing a name and the desired fault domain count (2 or 3). 

![](/azure/images/azure-availabilitysets-create.png)
<sub>*Full size [here](/azure/images/azure-availabilitysets-create.png).*</sub>

The sets defined here can be assigned to the hostgroups in `Choose Blueprint` tab. An availability set can be assigned to only one hostgroup so you should define as much availability set in advance as needed for your hostgroups. By default, there is no availability set selected. The assignment of fault domains is automated by Azure so there is no option in Cloudbreak.

  >**IMPORTANT:** Single instances placed in an Availability Set are not subject to Azure’s SLA, and you won’t receive warnings of planned maintenance events, so Availability Groups should only be used when there’s a group of two or more application tier VMs.


![](/azure/images/azure-availabilitysets-assign.png)
<sub>*Full size [here](/azure/images/azure-availabilitysets-assign.png).*</sub>

After the deployment is finished, the layout of the VM-s inside an availability set can be checked in Azure Portal. There are "Availability set" resources corresponding to the hostgroups inside the deployments's resource group.  

![](/azure/images/azure-availabilitysets-portal.png)
<sub>*Full size [here](/azure/images/azure-availabilitysets-portal.png).*</sub>

*Rack awareness*

Rack awareness is having the knowledge of Cluster topology or more specifically how the different data nodes are distributed across the racks of a Hadoop cluster. The importance of this knowledge relies on this assumption that co-located data nodes inside a specific rack will have more bandwidth and less latency whereas two data nodes in separate racks will have comparatively less bandwidth and higher latency.

The main purpose of Rack awareness are:

 - Increasing the availability of data block
 - Better cluster performance

HDFS replicates a data block into 3 replicas by default. In this configuration, 2 blocks stay rack local and one block is placed in a different rack. When building a Hadoop cluster on Azure there is no notion of a physical rack. However the fault domains are similar in the failure characteristics of a physical rack. Since electrical events affect a fault domain as an unit, it is important to assign the rack topology based on fault domain allocation.

You can view the rack assignment in Ambari, clicking on the Hosts menu item. If there was no availability set selected for the given host's hostgroup, it's rack remains set to "default rack".

![](/azure/images/azure-availabilitysets-rackawareness.png)
<sub>*Full size [here](/azure/images/azure-availabilitysets-rackawareness.png).*</sub>