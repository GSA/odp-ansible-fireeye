Role Name
=========

The ansible role `odp-ansible-fireeye` is used to install and configure the Fireeye endpoint security agent.

Requirements
------------

### OS Supported

* RHEL 7
* CentOS 7
* Amazon Linux 2
* Amazon EKS enhanced Linux ( Based on Amazon Linux 2 )
* Ubuntu releases running systemd ( 16.04, 18.04, etc )

### Requirements

* FireEye package available in your OS software repository or stored in an ***AWS*** S3 bucket
* FireEye certificates and credentials:
  * cacert
  * provocert
  * provokey

Role Variables
--------------
| Variable | Type | Description | Required |
| ---  | ---  | ---  | --- |
| fireeye_cacert | string   | FireEye HX CA Cert | true  |
| fireeye_provocert | string   | FireEye HX provocert | true  | 
| fireeye_provokey | string   | FireEye HX provokey . |  true |
| fireeye_servers | list   | List of FireEye HX server. | true |
| fireeye_package | string | FireEye HX package version to install. For S3 download use the full package name stored in S3. | true | 
| fireeye_s3_bucket | string   | Set ONLY if you are using an S3 bucket to store FireEye HX install package. | false  |
| fireeye_s3_prefix | string   | Set ONLY if you are using an S3 bucket to store FireEye HX  install package. | false  |

Dependencies
------------

* No external role dependencies

Example Playbook When Using OS Native Package Manager
----------------
```
- hosts: servers
  roles:
    - role: odp-ansible-fireeye
      fireeye_cacert: "123itsamystery"
      fireeye_provocert: "123itsamystery"
      fireeye_provokey: "123itsamystery"
      fireeye_servers: [ "1.1.1.1", "2.2.2.2"  ]
      fireeye_packge: xagt-32.30.0-1
```

Example when downloading install from S3 bucket

```
- hosts: servers
  roles:
- hosts: servers
  roles:
    - role: odp-ansible-fireeye
      fireeye_cacert: "123itsamystery"
      fireeye_provocert: "123itsamystery"
      fireeye_provokey: "123itsamystery"
      fireeye_servers: [ "1.1.1.1", "2.2.2.2"  ]
      fireeye_packge: xagt-32.30.0-1
      fireeye_s3_bucket: "ma_bucket"
      fireeye_s3_prefix: "my_prefix"

```

Todo
-------

* Currently the S3 copy to local happens ***EVERY*** time the role is deployed.  There needs to be a check, maybe with package_facts, to determine if the specific version of the package is installed and if so skip.  
  * This is potentially costly and time consuming if run outside of an image build pipeline.


License
-------

BSD

Author Information
------------------

GSA OCISO DevSecops Team - ociso-devsecops@gsa.gov
Github Repository - https://github.com/GSA/odp-ansible-cylance
