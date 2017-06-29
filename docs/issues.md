# Known issues

## Upgrade to 1.16.1

If you upgrade Cloudbreak to 1.16.1 and you don't have the `UAA_DEFAULT_SECRET` specified in the Profile, Cloudbreak deployer will generate one automatically. Furthermore, if you have existing clusters, Cloudbreak will use this new secret to decrypt the database records; however, those were encrypted with the old secret so the old secret needs to be provided in the Profile. 

**Workaround**: If you have an existing cluster without the `UAA_DEFAULT_SECRET` in your Profile, you must extend the Profile before starting Cloudbreak 1.16.1.

```export UAA_DEFAULT_SECRET=cbsecret2015```

This issue will be fixed in an upcoming release. 


## Decommission

* [AMBARI-15294](https://issues.apache.org/jira/browse/AMBARI-15294) In case of downscaling if the selected host group contains an HBase RegionServer it's not guaranteed that all regions will be safely moved to another RegionServer which will remain as part of the cluster. If you choose to scale down such a host group Cloudbreak won't track the region movement process. It is recommended to put the RegionServers in a different host group in your blueprint than the ones you'll be scaling.

## Cloudbreak Shell

* [EAR-5997](https://hortonworks.jira.com/browse/EAR-5997) NullPointerException will be thrown from CloudbreakShell during execution of ```stack create``` command if the template creation commands are executed after credential selection.<br>

Example:

```
credential select --name my-aws-credential
...
template create --AWS --name my-aws-template --description aws-template --instanceType m3.large --volumeType ephemeral --volumeCount 1 --volumeSize 32 --topologyId 1 --encrypted false
...
stack create --AWS --name my-aws-cluster --region eu-west-1
```

Workaround: template creation commands should be executed before the credential selection command

```
template create --AWS --name my-aws-template --description aws-template --instanceType m3.large --volumeType ephemeral --volumeCount 1 --volumeSize 32 --topologyId 1 --encrypted false
...
credential select --name my-aws-credential
...
stack create --AWS --name my-aws-cluster --region eu-west-1
```
