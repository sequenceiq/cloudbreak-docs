# Release Notes

The Release Notes document describes new features and fixes incorporated in this version of Cloudbreak.

## Improvements

This release includes the following improvements:

| Feature | Description |
|----|----|
| Designate Ambari Server Host Group (RMP-7026) | When creating a cluster, you can designate in which host group to include Ambari Server. |
| Azure: Support for New Regions (RMP-7028) | Support for Canada East and Canada Central. |

## Fixes & Changes

This release include the following changes:
> Refer to the [Change Log](changelog.md) for a full list of changes.

| Area | Change |
|---|---|
| Azure Cloud Provider | Reduce host name length on Azure in order to be sure that the hostname is under 64 chars. |
| Azure Cloud Provider | Azure VMs supporting private deployments (when VMs have private IP only.) |
| Azure Cloud Provider | Do not use the same host names for every cluster on Azure. |
| Azure Cloud Provider | Configurable stack name prefix length in Azure host names. |
| Networking | Rename all open port security group to denote unsecure. |
| Networking | Remove all port open security group as default. |

## Technical Preview

This release includes the following Technical Preview features and improvements:

| Feature | Description |
|----|----|
| Custom Images | **Technical Preview** Ability to set custom images. See [Cloud Images](images.md) for more information. |
| AWS: Spot Pricing | **Technical Preview** Support for configuring Spot Price with resource templates. |
| Mesos | **Technical Preview** Support for Mesos cloud provider. See [Mesos](mesos.md) for more information. |
| Kerberos | **Technical Preview** Support for enabling Kerberos on the HDP clusters deployed by Cloudbreak. See [Kerberos](kerberos.md) for more information. |
| Platforms | **Technical Preview** Support for defining Platforms to relate different configurations together. See [Platforms](topologies.md) for more information. |
| Ambari Database | **Technical Preview** Support for using an external database for Ambari. See [Ambari Database](database.md) for more information. |
