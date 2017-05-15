# Release Notes

The Release Notes document describes new features and fixes incorporated in this version of Cloudbreak.

## Improvements

This release includes the following improvements:

| Feature | Description |
|----|----|
| HDP and Ambari | Update to HDP 2.6 and Ambari 2.5. |
| Azure Support for Private IPs | Support for using Azure Private IPs. |

## Fixes & Changes

This release include the following changes:
> Refer to the [Change Log](changelog.md) for a full list of changes.

| Area | Change |
|---|---|
| Azure Cloud Provider | Deallocate VMs instead of just stopping the instances. |

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
