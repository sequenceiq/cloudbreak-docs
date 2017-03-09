## File System Configuration

When starting a cluster with Cloudbreak on Azure, the default file system is “Local HDFS”.

Cloudbreak has support for [Azure Data Lake Store (ADLS) file system](https://hadoop.apache.org/docs/r3.0.0-alpha2/hadoop-azure-datalake/index.html), selecting it from the drop-down list automatically configures the required properties in the cluster. ADLS is not supported as default file system.   

Hadoop has built-in support for the [Windows Azure Blob Storage (WASB) file system](https://hadoop.apache.org/docs/current/hadoop-azure/index.html), so it can be
used easily as default file system. To enable this behavior, `Use File System As Default` must be selected.

### Disks and Storage

In Azure every data disk attached to a virtual machine [is stored](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-disks-vhds/) as a virtual hard disk (VHD) in a page blob inside an Azure storage account. Because these are not local disks and the operations must be done on the VHD files it causes degraded performance when used as HDFS.
When WASB is used as a Hadoop file system the files are full-value blobs in a storage account. It means better performance compared to the data disks and the WASB file system can be configured very easily but Azure storage accounts have their own [limitations](https://azure.microsoft.com/en-us/documentation/articles/azure-subscription-service-limits/#storage-limits) as well. There is a space limitation for TB per storage account (500 TB) as well but the real bottleneck is the total request rate that is only 20000 IOPS where Azure will start to throw errors when trying to do an I/O operation.
To bypass those limits Azure Data Lake Store (ADLS) can be used, which is an Apache Hadoop file system compatible with Hadoop Distributed File System (HDFS) and works with the Hadoop ecosystem. To be able to use it, an ADLS account must be created on your Azure subscription. For more information on ADLS, refer to [Overview of Azure Data Lake Store](https://azure.microsoft.com/en-us/documentation/articles/data-lake-store-overview/).

### Containers Within the Storage Account

Cloudbreak creates a new container in the configured storage account for each cluster with the following name
pattern `cloudbreak-UNIQUE_ID`. Re-using existing containers in the same account is not supported as dirty data can
lead to failing cluster installations. In order to take advantage of the WASB file system your data does not have to
be in the same storage account nor in the same container. You can add as many accounts as you wish through Ambari, by
 setting the properties described [here](https://hadoop.apache.org/docs/stable/hadoop-azure/index.html). Once you
 added the appropriate properties you can use those storage accounts with the pre-existing data, like:
```
hadoop fs -ls wasb://data@youraccount.blob.core.windows.net/terasort-input/
```

> **IMPORTANT:** Make sure that your cloud account can launch instances using the new Azure ARM (a.k.a. V2) API and
you have sufficient qouta (CPU, network, etc) for the requested cluster size.
