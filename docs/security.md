# Cloudbreak Security

Security is very important at all, but most important in production environment. Cloudbreak delivers default settings, but those settings are purposing easy first dating, not security. So first of all what you can do is block all communication ports except 443 on the firewall / security group / what ever you use. Hardly recommended to open SSH port (usually 22) if you have to log in to the Cloudbreak host remotely.

Second step is to configure Profile before starting Cloudbreak for the first time. First execute the following command in the directory where you want to store Cloudbreak related files:
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
Cloudbreak has more additional secrets which by default inherits value from `UAA_DEFAULT_SECRET`, but you should also define different one in the Profile for each of the service clients:
```
export UAA_CLOUDBREAK_SECRET='[clousbreak secret]'
export UAA_PERISCOPE_SECRET='[auto scaling secret]'
export UAA_ULUWATU_SECRET='[web ui secret]'
export UAA_SULTANS_SECRET='[authenticator secret]'
```
You can change secrets any time except `UAA_CLOUDBREAK_SECRET`, because it is used to encrypt sensitive information in database level. Client secret changes are applied during start so restart required.

As you see `UAA_DEFAULT_USER_PW` is stored in plain text format, but if `UAA_DEFAULT_USER_PW` is missing it gets a default value. Because default password is not an option if you set an explicit empty password in Profile, Cloudbreak deployer will ask for password all the time when password needed for the operation.
```
export UAA_DEFAULT_USER_PW=''
```
In that case Cloudbreak deployer couldn't add default user, so you have to do it manually by executing the following command:
```
cbd util add-default-user
```