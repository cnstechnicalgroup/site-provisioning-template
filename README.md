site-provisioning-template
========

Starter ansible template for new site project. All required variables should be defined in the management_vpc
playbook.

Requirements
------------

Nothing, it runs out of the box.

Variables
--------------

In the current version, you can specify the following variables:

| Name                  | Default |                                                                               |
|-----------------------|---------|-------------------------------------------------------------------------------|
| vpc                   |   ---   | Object containing entire VPC structure. Registered by [cns.vpc-info] role.    |
| mode                  |   ---   | Target build environment (dev, test, stage, prod.                             |
| mgmt_subnet_name      |   ---   | Name of the management subnet for the target VPC.                             |
| prefix                |   ---   | Short name for site. e.g. the-world.com becomes theworldcom.                  |
| domain                |   ---   | Primary site domain name. e.g. the-world.com.                                 |
| subdomain             |   ---   | Special environment subdomains for dev, test, and stage.                      |
| ssl_certificate_id    |   ---   | AWS IAM SSL Certificate ID.                                                   |
| dns                   |   ---   | Object variable containing Route 53 zone information. See [cns.dns].          |

Dependencies
------------

This package has no dependencies.

License
-------

GPLv2

Author Information
------------------

Created by Sam Morrison [@samcns](https://www.twitter.com/samcns)

Examples
--------

```yaml
---
- hosts: localhost
  connection: local
  vars_files:
    # Target VPC identifiers (keep out of public repos)
    - ../../vars/vpc_details.yml
    # Region specific Security Group identifiers
    - ../../vars/global_sg_details.yml
  roles:
    - cns.vpc-info
    - { role: cns.provisioning-sg,
        prefix: 'theworldcom',
        domain: 'the-world.com',
        subdomain: 'dev001',
        mode: 'dev' }
    - { role: cns.provisioning-sg,
        prefix: 'theworldcom',
        domain: 'the-world.com',
        subdomain: 'test001',
        mode: 'test' }
    - { role: cns.provisioning-sg,
        prefix: 'theworldcom',
        domain: 'the-world.com',
        subdomain: 'stage001',
        mode: 'stage' }
    - { role: cns.provisioning-sg,
        prefix: 'theworldcom',
        domain: 'the-world.com',
        subdomain: 'www',
        mode: 'prod' }
    - cns.dns
```

[cns.vpc-info]: https://github.com/cnstechnicalgroup/role-vpc-info
[cns.dns]: https://github.com/cnstechnicalgroup/role-dns
