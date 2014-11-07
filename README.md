# <a name="title"></a> Kitchen::Opennebula

A Test Kitchen Driver for Opennebula.

## <a name="requirements"></a> Requirements

This driver depends on BlackBerry patches to Fog (https://github.com/fog/fog)
for better support for OpenNebula.  These patches can be found at
https://github.com/blackberry/fog until they are merged to upstream.

## <a name="installation"></a> Installation and Setup

Please read the [Driver usage][driver_usage] page for more details.

## Virtual Machine Requirements

This driver requires an OpenNebula OS image that conforms to a number of requirements

* The VM puts the ssh key defined in the SSH\_PUBLIC\_KEY context variable into `$HOME/.ssh/authorized_keys`
* The VM ensures the user has passwordless sudo access

## <a name="config"></a> Configuration

### <a name="opennebula_endpoint"></a> opennebula\_endpoint

URL where the OpenNebula daemon is listening.  
The default value is taken from the ONE\_XMLRPC environment variable, or `http://127.0.0.1:2633/RPC2` if unset.

### <a name="oneauth_file"></a> oneauth\_file

Path to the file containing OpenNebula authentication information.  It should contain a single line stating "username:password".
The default value is taken from the ONE\_AUTH environment variable, or `$HOME/.one/one_auth` if unset.

### <a name="template_name"></a> template\_name

Name of the VM definition file (OpenNebula template) registered with OpenNebula.  Can be used with `template_uname` or `template_uid` to further restrict which template to use if multiple users have the same template name.  Only one of `template_name` or `template_id` must be specified in the .kitchen.yml file.
The default value is unset, or `nil`.

### <a name="template_id"></a> template\_id

ID of the VM definition file (OpenNebula template) registered with OpenNebula.  Only one of `template_name` or `template_id` must be specified in the .kitchen.yml file.
The default value is unset, or `nil`.

### <a name="template_uname"></a> template\_uname

Username who owns the VM definition file (OpenNebula template).  Can be used with `template_name` to address naming conflicts where multiple users have the same template name.
The default value is unset, or `nil`.

### <a name="template_uid"></a> template\_uid

UID of the user who owns the VM definition file (OpenNebula template).  Can be used with `template_name` to address naming conflicts where multiple users have the same template name.
The default value is unset, or `nil`.

### <a name="vm_hostname"></a> vm\_hostname

Hostname to set for the newly created VM.
The default value is `driver.instance.name`

### <a name="public_key_path"></a> public\_key\_path

Path to SSH public key to pass to the VM, to use to authenticate with `username` when logging in or converging a node.
The default value is `~/.ssh/id_rsa.pub`, `~/.ssh/id_dsa.pub`, `~/.ssh/identity.pub`, or `~/.ssh/id_ecdsa.pub`, whichever is present on the filesystem.

### <a name="username"></a> username

This is the username used for SSH authentication to the new VM.
The default value is `local`.

### <a name="memory"></a> memory

The amount of memory to provision for the new VM.  This parameter will override the memory settings provided in the VM template.
The default value is 512MB.

### <a name="user_variables"></a> user\_variables

A hash of variables to pass into the "user template" section of the VM, to customize the virtual machine.
The default value is `{}`.

### <a name="context_variables"></a> context\_variables

A hash of variables to pass into the "CONTEXT" section of the VM, to further customize the virtual machine.  These variables override any existing context variables that are provided as part of the specified VM template.
The default value is `{}`.

### <a name="config-require-chef-omnibus"></a> require\_chef\_omnibus

Determines whether or not a Chef [Omnibus package][chef_omnibus_dl] will be
installed. There are several different behaviors available:

* `true` - the latest release will be installed. Subsequent converges
  will skip re-installing if chef is present.
* `latest` - the latest release will be installed. Subsequent converges
  will always re-install even if chef is present.
* `<VERSION_STRING>` (ex: `10.24.0`) - the desired version string will
  be passed the the install.sh script. Subsequent converges will skip if
  the installed version and the desired version match.
* `false` or `nil` - no chef is installed.

The default value is unset, or `nil`.

## <a name="development"></a> Development

* Source hosted at [GitHub][repo]
* Report issues/questions/feature requests on [GitHub Issues][issues]

Pull requests are very welcome! Make sure your patches are well tested.
Ideally create a topic branch for every separate change you make. For
example:

1. Fork the repo
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## <a name="authors"></a> Authors

Created and maintained by [Andrew Brown][author] (<anbrown@blackberry.com>)

## <a name="license"></a> License

Apache 2.0 (see [LICENSE][license])


[author]:           https://github.com/andrewjamesbrown
[issues]:           https://github.com/test-kitchen/kitchen-opennebula/issues
[license]:          https://github.com/test-kitchen/kitchen-opennebula/blob/master/LICENSE
[repo]:             https://github.com/test-kitchen/kitchen-opennebula
[driver_usage]:     http://docs.kitchen-ci.org/drivers/usage
[chef_omnibus_dl]:  http://www.getchef.com/chef/install/
