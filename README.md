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
| vpc                   |   ---   | Object containint entire VPC structure. Passed from management_vpc playbook.  |
| mode                  |   ---   | Target build environment (dev, test, stage, prod.                             |
| mgmt_subnet_name      |   ---   | Name of the management subnet for the target VPC.                             |
| prefix                |   ---   | Short name for site. e.g. the-world.com becomes theworldcom.                  |
| domain                |   ---   | Primary site domain name. e.g. the-world.com.                                 |
| subdomain             |   ---   | Special environment subdomains for dev, test, and stage.                      |
| ssl_certificate_id    |   ---   | AWS IAM SSL Certificate ID.                                                   |

Dependencies
------------

This package has no dependencies.

License
-------

GPLv2

Author Information
------------------

Created by Sam Morrison
https://www.twitter.com/samcns

Examples
--------

```yaml
# Include this in the management_vpc playbook.

- include: site-name/site.yml vpc: vpc, mode: 'dev', mgmt_subnet_name: 'management-subnet-001', prefix: 'theworldcom', domain: 'the-world.com', subdomain: 'dev', ssl_certificate_id: 'arn:aws:iam::012345678901:server-certificate/scert'
```
