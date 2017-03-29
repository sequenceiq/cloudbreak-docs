## Azure Access Setup

If you do not have an **Active Directory (AD)** user then you have to configure it before deploying a cluster with 
Cloudbreak:

> Why you need this? Read more [here](https://azure.microsoft.com/en-us/services/active-directory/)

 - Go to `manage.windowsazure.com` > `Active Directory`
 - Select one of your AD where you would like to create the new user
 - You can configure your AD users on `Your active directory` > `Users` menu

![](/azure/images/azure-aduser_v2.png)
<sub>*Full size [here](/azure/images/azure-aduser_v2.png).*</sub>

 - Here you can add the new user to AD. Simply click on `Add User` in the bottom of the page
    * `TYPE OF USER`: select `New user in your organization`
    * `USER NAME`: type the new user name into the box
    * Fill out the name fields for the new user on the second page of the ADD USER window
    * Submit the new user creation on the third window with the big green button
    * Copy the password `Folo4965`
    * Click on the tick button in the bottom of the the ADD USER window
 - You will see the new user in the `USERS` list

>You have got a temporary password so you have to change it before you start using the new user.

 - You need to add your AD user to the `manage.windowsazure.com` > `Settings` > `Administrators`

![](/azure/images/azure-administrators_v3.png)
<sub>*Full size [here](/azure/images/azure-administrators_v3.png).*</sub>

 - Here you can add the new user to Administrators. Simply click on `Add` in the bottom of the page
    * `EMAIL ADDRESS`: copy the previously created user email address here
    * Select the appropriate `SUBSCRIPTION` for the user
    * Click on the tick button in the bottom of the the ADD A CO-ADMINISTRATOR window
 - You will see the new co-administrator a in the `ADMINISTRATORS` list

## Azure Application Setup with Azure CLI

In order for Cloudbreak to be able to launch clusters on Azure on your behalf you need to set up your **Azure ARM 
application**. If you do not want to create your ARM application via the Azure Web UI, **you can create it with Azure CLI**.

You can find Azure CLI install documentation on the following link:
[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)

First you have to login with the command below:

```az login```

Then you can setup your Azure Application with the following Azure CLI command:

```
az ad sp create-for-rbac --name cloudbreak-app --password "****" --role Owner
```

Response:
```
{
  "appId": "********-748c-4018-b445-************",
  "displayName": "cloudbreak-app",
  "name": "http://cloudbreak-app",
  "password": "****",
  "tenant": "********-d98e-4c64-9301-************"
}
```

>  Why you need this? Read more [here](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-configure/)

1. It creates an Active Directory application with the configured name, password
2. It grants permissions to call the Azure Resource Manager API

**Please use the output of the command when you creating your Azure credential in Cloudbreak.**
