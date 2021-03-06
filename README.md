    #     ___  ____     _    ____ _     _____
    #    / _ \|  _ \   / \  / ___| |   | ____|
    #   | | | | |_) | / _ \| |   | |   |  _|
    #   | |_| |  _ < / ___ | |___| |___| |___
    #    \___/|_| \_/_/   \_\____|_____|_____|
***
## Manage instances with multiple attached volumes
This example launches 3 instances and attaches 2 volumes per instance.

This is done using Terraform's [interpolation syntax](https://www.terraform.io/docs/configuration/interpolation.html) for `count` variables and `math` operations.

The example also includes a user-data script in the instance launch, remote executes a command on each instance to setup the volumes, and outputs the public and private IP address of the instances.

### Using this example
* Update env-vars with the required information. Most examples use the same set of environment variables so you only need to do this once.
* Source env-vars
  * `$ . env-vars`
* Update `variables.tf` with your instance options. You may also modify the `NumInstances` and `NumVolumesPerInstance` variables to change the number of instances and volumes that are launched.

### Files in the configuration

#### `env-vars`
Is used to export the environmental variables used in the configuration. These are usually authentication related, be sure to exclude this file from your version control system. It's typical to keep this file outside of the configuration.

Before you plan, apply, or destroy the configuration source the file -  
`$ . env-vars`

#### `block.tf`
Defines the volumes that are attached to the compute instances.

#### `compute.tf`
Defines the compute resource. This demo connects to the running instance 
so you will need to supply public/private keys to create an ssh connection. 
**NOTE**: do not try to use your api keys, see [this doc](https://docs.us-phoenix-1.oraclecloud.com/Content/Compute/Tasks/managingkeypairs.htm)
for more info on configuring keys.

#### `remote-exec.tf`
Uses a `null_resource`, `remote-exec` and `depends_on` to execute a command on the instance. [More information on the remote-exec provisioner.](https://www.terraform.io/docs/provisioners/remote-exec.html) 

#### `./userdata/bootstrap`
The user-data script that gets injected into the instance on launch. More information on user-data scripts can be [found at the cloud-init project.](https://cloudinit.readthedocs.io/en/latest/topics/format.html)

#### `variables.tf`
Defines the variables used in the configuration

#### `datasources.tf`
Defines the datasources used in the configuration

#### `outputs.tf`
Defines the outputs of the configuration

#### `provider.tf`
Specifies and passes authentication details to the OCI TF provider
