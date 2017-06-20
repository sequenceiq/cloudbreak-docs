# Get Help

## Options for Getting Help

If you need help with Cloudbreak, you have two options:

| Option | Description |
|---|---|
| Hortonworks Community Connection |	This is free optional support via Hortonworks Community Connection (HCC).|
| Hortonworks Flex Support Subscription | This is paid Hortonworks enterprise support.|

## HCC

You can optionally register for optional free community support at [Hortonworks Community Connection](https://community.hortonworks.com/answers/index.html) where you can browse articles and previously answered questions, and ask questions of your own. When posting questions related to Cloudbreak, make sure to use the "Cloudbreak" tag.

## Flex Subscription

You can optionally use your existing Hortonworks [Flex subscription(s)](https://hortonworks.com/services/support/enterprise/) to cover the Cloudbreak node and all clusters created. 

**Prerequisites**: You must have an existing SmartSense ID and a Flex subscription. For general information about the Hortonworks Flex Support Subscription, visit the Hortonworks Support page at [https://hortonworks.com/services/support/enterprise/](https://hortonworks.com/services/support/enterprise/).

The general steps are:

1. Configure Smart Sense in your `Profile` file.   
2. Register your Flex subscription in the Cloudbreak web UI in the the **manage flex subscriptions** pane. You can register and manage multiple Flex subscriptions.  

Once you've performed these steps: 

* In the the **manage flex subscriptions** pane, you can assign your registered Flex subscription to the Cloudbreak node and set it as default for newly created clusters.  
* When creating a cluster using the advanced options, you can select the Flex subscription that you want to use.  
This option is available in the **CONFIGURE CLUSTER** > **Flex Subscriptions** section of the create cluster form.  

Alternatively, you can perform these steps using the Cloudbreak Shell. 


### Configuring SmartSense

To configure SmartSense in Cloudbreak, enable SmartSense and add your SmartSense ID to the `Profile` by adding the following variables:

<pre>export CB_SMARTSENSE_CONFIGURE=true
export CB_SMARTSENSE_ID=YOUR-SMARTSENSE-ID</pre>
    
For example:
 
<pre>export CB_SMARTSENSE_CONFIGURE=true
export CB_SMARTSENSE_ID=A-00000000-C-00000000</pre>

You can do this in one of the two ways:

* When initiating Cloudbreak Deployer  
* After you've already initiated Cloudbreak Deployer. If you choose this option, you must restart Cloudbreak using `cbd restart`.

> SmartSense ID defined in the `Profile` file always overrides the ID registered via Cloudbreak Shell.


### Managing Flex Subscriptions

Once you log in to the Cloudbreak web UI, you can manage your Flex subscriptions from the **manage flex subscriptions** pane. You can:

* Register a new Flex subscription.  
* Set a default Flex subscription.  
* Select a Flex subscription to be used for cloud controller.  
* Delete a Flex subscription.  
* Check which clusters are connected to a specific subscription.  

When creating a cluster using the advanced options, in the **CONFIGURE CLUSTER** > **Flex Subscriptions**, you can select the Flex subscription that you want to use.


### Managing SmartSense and Flex Subscriptions via Cloudbreak Shell 

#### Configuring SmartSense via Cloudbreak Shell 
    
1. Enable SmartSense in the `Profile` by adding the following variable: 

    <pre>export CB_SMARTSENSE_CONFIGURE=true</pre>

2. You can use Cloudbreak Shell to configure SmartSense subscription on the fly. For example, to register a SmartSense ID `A-00000000-C-00000000` use:

    ```smartsense register --subscriptionId A-00000000-C-00000000```
 
    > SmartSense ID defined in the `Profile` file always overrides the ID registered via Cloudbreak Shell.

#### Managing SmartSense via Cloudbreak Shell 

Register SmartSense subscription:

```
smartsense register --subscriptionId A-00000000-C-00000000
```

Describe already registered SmartSense subscription:

```
smartsense describe
```

Delete SmartSense subscription:

```
smartsense delete --subscriptionId A-00000000-C-00000000
```


#### Managing Flex Subscriptions via Cloudbreak Shell

Register Flex subscription:

```
flex register --name my-flex-subscription --subscriptionId FLEX-0123456789
```

List already registered Flex subscriptions:

```
flex list
```

Describe an existing Flex subscription:

```
flex show --name my-flex-subscription
```

Set Flex subscription as default:

```
flex set-default --name my-flex-subscription
```

Use Flex subscription for Cloudbreak instance:

```
flex use-for-controller --name my-flex-subscription
```

Delete Flex subscription:

```
flex delete --name my-flex-subscription
```
