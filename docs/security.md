# Cloudbreak Security

Security is very important in general, but it is the most important in production environments. Cloudbreak comes with default settings, but those settings are aiming for easy first dating, not strict security. So first of all you can block all communication ports except 443 on the firewall / security group / whatever you use. It is strongly recommended to open SSH port (usually 22) if you have to log in to the Cloudbreak host remotely.

The second step is to configure the Profile file before starting Cloudbreak for the first time. As a starting point, execute the following command in the directory where you want to store Cloudbreak related files:
```
echo export PUBLIC_IP=[the ip or hostname to bind] > Profile
```
After you have a base Profile you should add custom properties to the Profile file:
```
export UAA_DEFAULT_SECRET='[custom secret]'
export UAA_DEFAULT_USER_EMAIL='[default admin email address]'
export UAA_DEFAULT_USER_PW='[default admin password]'
export UAA_DEFAULT_USER_FIRSTNAME='[default admin first name]'
export UAA_DEFAULT_USER_LASTNAME='[default admin last name]'
```
Cloudbreak has more additional secrets which by default inherits their values from `UAA_DEFAULT_SECRET`, but you should also define different ones in the Profile for each of the service clients:
```
export UAA_CLOUDBREAK_SECRET='[cloudbreak secret]'
export UAA_PERISCOPE_SECRET='[auto scaling secret]'
export UAA_ULUWATU_SECRET='[web ui secret]'
export UAA_SULTANS_SECRET='[authenticator secret]'
```
You can change secrets any time except `UAA_CLOUDBREAK_SECRET`, because it is used to encrypt sensitive information at database level. Client secret changes are applied during startup so a restart is required after a change.

As you see `UAA_DEFAULT_USER_PW` is stored in plain text format, but if `UAA_DEFAULT_USER_PW` is missing from the Profile, it gets a default value. Because default password is not an option if you set an empty password explicitly in the Profile, Cloudbreak deployer will ask for password all the time when it is needed for the operation.
```
export UAA_DEFAULT_USER_PW=''
```
In this case Cloudbreak deployer wouldn't be able to add the default user, so you have to do it manually by executing the following command:
```
cbd util add-default-user
```
