---

copyright:
  years: 2020, 2021
lastupdated: "2021-06-18"

keywords: commands, cluster resource, hpvs-cli plugin, hpvs CLI, hpvs-cli command line , hpvs-cli shell


subcollection: hpvs-cli-plugin

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}

# {{site.data.keyword.cloud_notm}} {{site.data.keyword.hpvs}} CLI
{: #hpvs_cli_plugin}

Use the {{site.data.keyword.hpvs}} CLI to list, create, or delete your {{site.data.keyword.cloud}} {{site.data.keyword.hpvs}} instances.
{:shortdesc}

The {{site.data.keyword.hpvs}} CLI is available for the amd64 architecture on Linux&reg;, Windows&reg;, and Mac.

## Prerequisites
{: #prerequisites_hpvs_cli_plugin}


- Install the [{{site.data.keyword.cloud_notm}} CLI](https://cloud.ibm.com/docs/cli?topic=cli-getting-started). The prefix for running commands by using the {{site.data.keyword.cloud_notm}} CLI is `ibmcloud`.

- Install the {{site.data.keyword.cloud_notm}} {{site.data.keyword.hpvs}} CLI by running the following command:

   ```sh
   ibmcloud plugin install hpvs
   ```
   {: pre}

If you want to view the current version of your {{site.data.keyword.hpvs}}
CLI plug-in, run `ibmcloud plugin show hpvs`.

You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and [plug-ins](https://cloud.ibm.com/docs/cli?topic=cli-plug-ins) are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
{: tip}

{{site.data.keyword.cloud_notm}} CLI requires Java&reg; 1.8.0. You can download the CLI from {{site.data.keyword.cloud_notm}} to use on your local system as a complement to the {{site.data.keyword.cloud_notm}} console.
{: note}

Do not use personal information, for example, your name, as the instance name or as part of the instance name. The data that you provide when you provision an instance or interact with the hpvs cli is not considered to be personal data or credentials.
Learn more about IBM Cloud Hyper Protect Virtual Servers' Data usage and Certifications [here](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=165C6EF0FFDA11E8BABD512A6952EE1F).
{:note}

## CLI commands
{: #plugin_use}

## hpvs help
{: #display_list}

This command displays a list of hpvs commands.

```
ibmcloud hpvs help
```
{: pre}


## hpvs instances
{: #instances_list}

This command lists all your {{site.data.keyword.hpvs}} instances.

```
ibmcloud hpvs instances [--output json]
```
{: pre}

### Command options
{: #instances_co}
<dl>
<dt>`--output`</dt>
<dd>Displays results in the requested format. The only valid value is `json`.</dd>
</dl>


## hpvs instance
{: #details_list}

This command shows details about the server instance.

```
ibmcloud hpvs instance (NAME | CRN) [--output json]
```
{: pre}


<dl>
<dt>`NAME`</dt>
<dd>The name of your new instance. An error message is displayed if you specify a NAME that is not unique, for example,

```
VS name 'ABC' is ambiguous: more than one VS exist for the provided name: [crn1 crn2].
```

Specify the `CRN` if your instance name is not unique.</dd>
<dt>`CRN`</dt>
<dd>The server's Cloud resource name (CRN). Specify the `CRN` if `NAME` is not unique. You can run the `ibmcloud hpvs instances` command to get the CRN.</dd>
</dl>

### Command options
{: #details_co}

<dl>
<dt>`--output`</dt>
<dd>Displays results in the requested format. The only valid value is `json`.</dd>
</dl>

### Example output
{: #details_eo}

```
Name                  hpvs-env-test
CRN                   crn:v1:staging:public:hpvs:dal13:a/1075962b93044362a562c8deebbfba2e:0b2df6e9-ec2c-4b4a-87dd-60f53f6a2a0d::
Location              dal13
Cloud tags
Cloud state           active
Server status         running
Plan                  Free
Public IP address     52.116.29.73
Internal IP address   172.17.151.218
Storage               50 GiB
Memory                2048 MiB
Processors            1 vCPUs
Image type            self-provided
Image OS              self-defined
Image name            de.icr.io/hpvs_test/ubuntu:v2
Environment           TEST_VAR=value
                      TEST_VAR2=value2
Last operation        update succeeded
```
### Example JSON output during provisioning
{: #json_eo}
```
{
  "name": "hpvs-env-test",
  "crn": "crn:v1:staging:public:hpvs:dal13:a/1075962b93044362a562c8deebbfba2e:0b2df6e9-ec2c-4b4a-87dd-60f53f6a2a0d::",
  "region_id": "dal13",
  "tags": [],
  "state": "active",
  "status": "running",
  "resource_plan_title": "Free",
  "resource_plan_id": "bb0005a1-ec13-4ee4-86f4-0c3b15a357d5",
  "public_ip": "52.116.29.73",
  "internal_ip": "172.17.151.218",
  "storage": 53687091200,
  "memory": 2147483648,
  "vcpu": 1,
  "image_type": "self-provided",
  "image_os": "self-defined",
  "image_name": "de.icr.io/hpvs_test/ubuntu:v2",
  "free_time_left": 2156814134,
  "environment": {
    "TEST_VAR": "value",
    "TEST_VAR2": "value2"
  },
  "last_operation": "update succeeded"
}
```

## hpvs instance-create
{: #create_instance}

This command creates a new {{site.data.keyword.hpvs}} instance.


```
ibmcloud hpvs instance-create NAME PLAN LOCATION [(--ssh SSH-KEY | --ssh-path SSH-KEY-PATH)] [(--rd REGISTRATION-DEFINITION | --rd-path REGISTRATION-DEFINITION-PATH)] [-i IMAGE-TAG] [-e ENV-CONFIG1 -e ENV-CONFIG2 ...] [-g RESOURCE-GROUP-ID] [-t TAG1 -t TAG2 ...] [--outbound-only]
```
{: codeblock}


<dl>
<dt>`NAME`</dt>
<dd>The name of your new instance.</dd>
<dt>`PLAN`</dt>
<dd>The pricing plan ID or plan name for your Hyper Protect Virtual Server instance, for example, the plan name `lite-s` or its corresponding plan ID `bb0005a1-ec13-4ee4-86f4-0c3b15a357d5`. To list all plans and IDs, run the `ibmcloud catalog service hpvs` command.</dd>
<dt>`LOCATION`</dt>
<dd>The location ID to deploy your Hyper Protect Virtual Server instance to. To list available locations, run the `ibmcloud catalog service hpvs` command.</dd>
</dl>

### Command options
{: #create_co}
<dl>
<dt>`--ssh SSH-KEY` </dt>
<dd>Public half of the SSH key to access the virtual server later. `--ssh` or `--ssh-path` is required when you use an IBM-provided image.</dd>
<dt>`--ssh-path SSH-KEY-PATH` </dt>
<dd>File path to the file that contains the public half of the SSH key to access the virtual server later. `--ssh` or `--ssh-path` is required when you use an IBM-provided image.</dd>
<dt>`--rd REGISTRATION-DEFINITION`</dt>
<dd>The encrypted and signed registration definition that is used for [Bring your own server image (BYOI)](https://cloud.ibm.com/docs/hp-virtual-servers?topic=hp-virtual-servers-byoi). `--rd` or `--rd-path` is required when you use a self-provided image.</dd>
<dt>`--rd-path REGISTRATION-DEFINITION-PATH`</dt>
<dd>File path to the file that contains the encrypted and signed registration definition that is used for BYOI. `--rd` or `--rd-path` is required when you use a self-provided image.</dd>
<dt>`-i IMAGE-TAG`</dt>
<dd>The image tag for the BYOI server image. Required if you're using your own image.</dd>
<dt>`-t TAG` </dt>
<dd>Use tags to organize your resources. Tags are visible account-wide. Optional. Multiple tags are permitted, for example, `-t tag1 -t tag2`.</dd>
<dt>`-g RESOURCE-GROUP-ID | RESOURCE-GROUP-NAME` </dt>
<dd>The resource group to which your {{site.data.keyword.hpvs}} instance belongs for access control and billing purposes, for example, `Default`. To list all of your resource groups, run `ibmcloud resource groups`. Optional.</dd>
<dt>`-e ENV-CONFIG`</dt>
<dd>Specify environment variables if you are using a self-provided image. You must specify the variables in your registration definition first. You can set one or more environment variables as key value pairs by using the `-e` flag, for example, `-ibmcloud hpvs instance-update CRN -i latest -e k1=v1 -e k2='v2 v3'`. Environment variable `names` can have a maximum length of 64 characters and can be numbers, chars, and underscore. Environment variable `values` can have a maximum length of 4096.
</dd>
<dt>`--outbound-only`</dt>
<dd>If this parameter is set, only outbound connections are allowed from your Hyper Protect Virtual Server instance. Use the internal IP address to connect to this Virtual Server from other Virtual Servers created by the same {{site.data.keyword.cloud_notm}} account in the same region.</dd>
</dl>


### Example input
{: #create_ei}

```
ibmcloud hpvs instance-create MyHPVS lite-s dal13 -g Default --ssh "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCgguQtzV39LpP/iHAtjwo+4Z5QdASG73dwBlFIsTn5kPOaVYFHhzhvA/xMbLqDpxfYP/YzwU4rXNXMhCr4hlsruPXt5Ak4y83GmnNL8e+oq8lxU/afymje4PcYLnkm8WQvkreIEBaB73VOUKiLSSbdVljUk6a1LB347bCf72Oob8JpY4Pb3N4idrigSoCc+V4JVkz4pXD2Hoyar4J5I2527Ho+vUqdf5FoK9mFRUqtI8NTLKynL2/qVsCgTeUxnOknDjPE0+nqwyNI4toYozcISYb63K9Je6UBT4JaIQXMbdMhDH00wVH7R26SamKqS2iazcUBnZgN4//Vnic+US90ybsqvTuP/OQpHXwfdjshOEsz5PULZKbWgidsfA7aW3pjv1uijCPIrTFOsaAPktMCzhfJzaeFC0VIXweN7/2PT/Zl7U9Ys36CmmLaXfLotXxPWmbGUyRfavPN1Znhqph7v9w94E7JcngQ7sn+l+nkpYg5qdcBFZZ3kNhT4PVRbXE="
```

### Example output
{: #create_eo}

```
OK
Provisioning request for service instance 'crn:v1:staging:public:hpvs:dal13:a/1075962b93044362a562c8deebbfba2e:98338d1f-910b-4895-9410-453a9c4d9709::' was accepted.
 To check the provisioning status run:
 ibmcloud hpvs instance crn:v1:staging:public:hpvs:dal13:a/1075962b93044362a562c8deebbfba2e:98338d1f-910b-4895-9410-453a9c4d9709::
 ```

## hpvs instance-update
{: #hpvsinstanceupdate}

This command updates a Hyper Protect virtual server instance.

```
ibmcloud hpvs instance-update (NAME | CRN)  [(--rd REGISTRATION-DEFINITION | --rd-path REGISTRATION-DEFINITION-PATH)] [-i IMAGE-TAG] [-e ENV-CONFIG1 -e ENV-CONFIG2 ...] [--force]
```

{: pre}

<dl>
<dt>`NAME`</dt>
<dd>The name of your new instance. An error message is displayed if you specify a NAME that is not unique, for example,

```
VS name 'ABC' is ambiguous: more than one VS exist for the provided name: [crn1 crn2].
```

Specify the `CRN` if your instance name is not unique.</dd>
<dt>`CRN`</dt>
<dd>The server's Cloud resource name (CRN). Specify the `CRN` if `NAME` is not unique. You can run the `ibmcloud hpvs instances` command to get the CRN.</dd>
</dl>


### Command options
{: #details_iu}

<dl>
<dt>`--rd REGISTRATION-DEFINITION`</dt>
<dd>The encrypted and signed registration definition that is used for [Bring your own server image (BYOI)](https://cloud.ibm.com/docs/hp-virtual-servers?topic=hp-virtual-servers-byoi). `--rd` or `--rd-path` is optional when you use a self-provided image.</dd>
<dt>`--rd-path REGISTRATION-DEFINITION-PATH`</dt>
<dd>File path to the file that contains the encrypted and signed registration definition that is used for BYOI. `--rd` or `--rd-path` is optional when you use a self-provided image.</dd>
<dt>`-i IMAGE-TAG`</dt>
<dd>The image tag for the BYOI server image. Required if you're using your own image.</dd>
<dt>`-e ENV-CONFIG`</dt>
<dd>Specify environment variables when you use a self-provided image. They need to be specified in your registration definition first. You can set one or more environment variables as key value pairs by using the `-e` flag, for example, `-ibmcloud hpvs instance-update CRN -i latest -e k1=v1 -e k2='v2 v3'`. Environment variable `names` can have a maximum length of 64 characters and can be numbers, chars, and underscore. Environment variable `values` can have a maximum length of 4096.</dd>
<dt>`--force`</dt>
<dd>Forces the update of the {{site.data.keyword.hpvs}} instance without prompting for confirmation.</dd>
</dl>

{:note}
To check the status of the update, run `ibmcloud hpvs instance CRN` and check the value of `last operation` in the output.

## hpvs instance-delete
{: #hpvsinstance_delete}

This command deletes a {{site.data.keyword.hpvs}}.

```
ibmcloud hpvs instance-delete (NAME | CRN)
```
{: codeblock}

### Command options
{: #delete_co}

<dl>
<dt>`NAME`</dt>
<dd>The name of your new instance. An error message is displayed if you specify a NAME that is not unique, for example,

```
VS name 'ABC' is ambiguous: more than one VS exist for the provided name: [crn1 crn2].
```

Specify the `CRN` if your instance name is not unique.</dd>
<dt>`CRN`</dt>
<dd>The server's Cloud resource name (CRN). Specify the `CRN` if `NAME` is not unique. You can run the `ibmcloud hpvs instances` command to get the CRN.</dd>
<dt>`--force`</dt>
<dd>Forces the deletion of the {{site.data.keyword.hpvs}} instance without prompting for confirmation.</dd>
</dl>

### Example output
{: #delete_eo}

```
Are you sure you want to delete the service instance? [y/N]> y

Deleting service instance crn:v1:staging:public:hpvs:dal13:a/1075962b93044362a562c8deebbfba2e:231fbbf4-1415-4162-86f0-9d50c260106d:: ...

OK
Service instance 'crn:v1:staging:public:hpvs:dal13:a/1075962b93044362a562c8deebbfba2e:231fbbf4-1415-4162-86f0-9d50c260106d::' was deleted.
You can restore a resource within 7 days after you delete it.
You can run the 'ibmcloud resource reclamations' command to check the resources that you can restore.
To irrecoverable delete the instance run the 'ibmcloud resource reclamation-delete RECLAMATION_ID' command.
```


{:note}
When you delete a virtual server from the resource list, the server isn't deleted immediately, it stops and is marked for deletion. It is deleted after a reclamation period of seven days. During this seven-day reclamation period, you can restore the virtual server or manually trigger a deletion thru [resource reclamations](https://cloud.ibm.com/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_reclamations){: external}.



## hpvs registration-key-create
{: #hpvsregistrationkeycreate}

This command creates a Hyper Protect virtual server gpg registration key. The resulting output files are required inputs for the `hpvs registration-create` command, where it is used to sign the registration definition file for the deployment that uses your own image.

```
ibmcloud hpvs registration-key-create ID [--gpg-passphrase-path FILE-PATH] [-v VERBOSE]
```
{: pre}

<dl>
<dt>`ID`</dt>
<dd>The user ID to set for the gpg registration key.
</dd>
</dl>


### Command options
{: #reggpgdetails}

<dl>
<dt>`--gpg-passphrase-path FILE-PATH` </dt>
<dd>Is the path for the file that contains the passphrase that is being used for the registration key. The passphrase must consist of at least 6 characters. To make sure that a new line is not appended, use `echo` with `-n` or cat with EOF. If the path is not specified, you are prompted for the passphrase.</dd>
<dt>`-v, --verbose`</dt>
<dd>Set to true for verbose output.</dd>
</dl>

### Example output
{: #create_regkey}
```
$ ibmcloud hpvs registration-key-create abcdefg
Enter password>
Successfully created registration key batch file 'abcdefg_registration-batch.txt' in the current working directory.

Successfully generated registration key with gpg.

Successfully exported the public part of the registration key to 'abcdefg.public' in the current working directory.

Successfully exported the private part of the registration key to 'abcdefg.private' in the current working directory.

To use this registration key to generate a registration definition file run 'ibmcloud hpvs registration-create --registration-key-public-path abcdefg.public --registration-key-private-path abcdefg.private
```

## hpvs registration-create
{: #hpvsregistrationfilecreate}

This command creates a registration definition file that is required to instantiate a Hyper Protect Virtual Server based on an own image.

```
ibmcloud hpvs registration-create [--repository-name REPO-NAME] [--cr-username USER-NAME --cr-pwd-path FILE-PATH | --no-auth] [--allowed-env-keys ENV-KEYS | --no-env] [--image-key-id IMAGE-KEY-ID] [--image-key-public-path PUBLIC-KEY] [--registration-key-private-path PRIVATE-KEY-PATH] [--registration-key-public-path PUBLIC-KEY-PATH] [--gpg-passphrase-path PASS-PHRASE] [--cap-add CAPABILITIES]
```
{: pre}

If you enter the command without any parameters:

```
ibmcloud hpvs registration-create
```
{: pre}
you are prompted to enter all the parameters.

If the container registry does not require authentication, set the `-no-auth` parameter to prevent prompting. If no environment parameters are required, set the `-no-env` parameter, for example:

```
ibmcloud hpvs registration-create --no-env --no-auth
```
{: pre}

### Command options
{: #regfiledetails}

<dl>
<dt>`--repository-name REPO-NAME`</dt>
<dd>Is the fully qualified name for the repository.</dd>
<dt>`--cr-username USER-NAME`</dt>
<dd>Is the username for the login on the container repository. It can be any string of 4 - 30 characters.</dd>
<dt>`--cr-pwd-path FILE-PATH`</dt>
<dd>Is the path to the file that contains the container repository password.</dd>
<dt>`--no-auth`</dt>
<dd>Is the parameter that must be set if the image does not require authorization to download. In this case, you don't need to provide `cr-username` and `cr-pwd-path` parameters. If you do, these parameters are ignored. </dd>
<dt>`--allowed-env-keys ENV-KEYS`</dt>
<dd>Specifies the allowed environment variable keys as a comma-separated list. The keys must be strings of 1 - 64 characters.</dd>
<dt>`--no-env`</dt>
<dd>This parameter can be set if the image does not require any allowed environment variables. In this case, you don't need to provide the `allowed-env-keys` parameter. If you do, it is ignored.</dd>
<dt>`--image-key-id IMAGE-KEY-ID`</dt>
<dd>The ID of the root key that was used to sign the image. It must contain 64 characters. If the image-key-id is not specified, the command first tries to determine the ID automatically by requesting the container registry notary service. Optional.</dd>
<dt>`--image-key-public-path PUBLIC-KEY`</dt>
<dd>The path for the file that contains the public part of the key that was used to sign the image. The public part of the key must be a minimum of 20 characters and base64 encoded. If the path is not specified, the command first tries to determine the public part of the key automatically by requesting the container registry notary service. Optional.</dd>
<dt>`--registration-key-public-path PRIVATE-KEY-PATH`</dt>
<dd>The path for the public key from the registration key pair.</dd>
<dt>`--registration-key-private-path PUBLIC-KEY-PATH`</dt>
<dd>The path for the private key from the registration key pair.</dd>
<dt>`--gpg-passphrase-path PASS-PHRASE`</dt>
<dd>The path to a file that contains the `gpg` passphrase used for the private part of the registration key. The passphrase must consist of at least 6 characters. To make sure that a new line is not appended, use `echo` with `-n` or `cat` with EOF. </dd>
<dt>`--cap-add CAPABILITIES`</dt>
<dd>The Linux capabilities to be enabled are specified as a comma separated list.</dd>  
</dl>

### Example output
{: #create_regfile}

In this sample, the registration-key-create command is run with some, but not all, parameters. The output (the last line in sample) shows the command with all parameters.
You are prompted for the password and the gpg pass phrase. You must use the path to a file that contains the password for the `--cr-pwd-path parameter` and the path to a file that contains the pass phrase for the `--gpg-passphrase-path` parameter. The sample command contains placeholders for those paths.

```
$ ibmcloud hpvs registration-create --registration-key-public-path abcdefg.public --registration-key-private-path abcdefg.private
Repository name> docker.io/containers/your-image
Container registry user name> username
Container registry password>
Allowed environment variables as comma separated list> ENV_PARAM
Allowed Linux capabilities to be enabled as comma separated list> AUDIT_CONTROL,AUDIT_WRITE
Gpg pass phrase for the private part of the registration key>
OK
The registration file was successfully created in the current working directory: registration.json.asc
Complete command executed:
 ibmcloud hpvs registration-create --repository-name=docker.io/containers/your-image --cr-username=username --cr-pwd-path=<PATH> --allowed-env-keys="ENV_PARAM" --registration-key-public-path=abcdefg.public --cap-add=AUDIT_CONTROL,AUDIT_WRITE --registration-key-private-path=abcdefg.private --gpg-passphrase-path=<PATH>
 ```
