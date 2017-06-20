# Get Help

## Options for Getting Help

If you need help with Cloudbreak, you have two options:

| Option | Description |
|---|---|
| Hortonworks Community Connection |	This is free optional support via Hortonworks Community Connection.|
| Hortonworks Flex Support Subscription | This is paid Hortonworks enterprise support.|

## HCC

You can optionally register for optional free community support at [Hortonworks Community Connection](https://community.hortonworks.com/answers/index.html) where you can browse articles and previously answered questions, and ask questions of your own. When posting questions related to Cloudbreak, make sure to use the "Cloudbreak" tag.

## Flex Subscription

You can optionally use your existing Hortonworks [Flex Subscriptions](https://hortonworks.com/services/support/enterprise/) to cover the Cloudbreak node and all clusters created. To do that you must:

1. Configure SmartSenseID and Telemetry in your `Profile` file.   
2. Register your Flex Subscription in the Cloudreak web UI.

Once you've performed these steps, your Flex subscription can be used for the Cloudbreak node and all newly created clusters. You can register multiple subscriptions and manage them in the cloud controller UI.

For general information about the Hortonworks Flex Support Subscription, visit the Hortonworks Support page at [https://hortonworks.com/services/support/enterprise/](https://hortonworks.com/services/support/enterprise/).

### Configuring SmartSense Subscription

To configure Flex in Cloudbreak, you have to enable SmartSense in the `Profile` by adding the following variable:

    <pre>export CB_SMARTSENSE_CONFIGURE=true</pre>

You can do this in one of the two ways:

* When initiating Cloudbreak  
* After you've already initiated Cloudbreak Deployer. In this case, you must restart Cloudbreak using `cbd restart`.

After you are done, you have two options to manage SmartSense subscription:

 1. You can define SmartSense subscription id in your `Profile` like `CB_SMARTSENSE_CONFIGURE`.

    <pre>export CB_SMARTSENSE_ID=YOUR-SMARTSENSE-ID</pre>

    For example:
 
    <pre>export CB_SMARTSENSE_ID=A-00000000-C-00000000</pre>

> Restarting Cloudbreak is mandatory after `Profile` changed.

 2. You should use Cloudbreak Shell to configure SmartSense subscription on the fly.
 
 > SmartSense subscription id defined in `Profile` file always override subscription created via Cloudbreak Shell.

#### Register SmartSense subscription

```
smartsense register --subscriptionId A-00000000-C-00000000
```

#### Describe already registered SmartSense subscription

```
smartsense describe
```

#### Delete SmartSense subscription

```
smartsense delete --subscriptionId A-00000000-C-00000000
```

### Managing Flex Subscriptions

Once you log in to the Cloudbreak web UI, you can manage your Flex subscriptions from the manage Flex subscriptions tab. From this tab, you can:

* Register a new Flex subscription.  
* Set a default Flex subscription.  
* Select a Flex subscription to be used for cloud controller.  
* Delete a Flex subscription.  
* Check which clusters are connected to a specific subscription.  

When creating a cluster using the advanced options, in the **CONFIGURE CLUSTER** > **Flex Subscriptions**, you can select the Flex subscription that you want to use.

Equivalent options are also available via Cloudbreak Shell.

#### Register Flex subscription

```
flex register --name my-flex-subscription --subscriptionId FLEX-0123456789
```

#### List already registered Flex subscriptions

```
flex list
```

#### Describe an existing Flex subscription

```
flex show --name my-flex-subscription
```

#### Set Flex subscription as default

```
flex set-default --name my-flex-subscription
```

#### Use Flex subscription for Cloudbreak instance

```
flex use-for-controller --name my-flex-subscription
```

#### Delete Flex subscription

```
flex delete --name my-flex-subscription
```