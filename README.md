tf-aws-ebs-environment
----------------

This simple module is designed to:
* create Elastic Beanstalk environment inside provided application (inside VPC)

**This module is designed to work with Elastic Beanstalk Docker platforms.**

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| app | App name. | string | - | yes |
| app_solution_stack | Solution stack to be used. | string | - | yes |
| app_tier | Webserver or Worker. | string | `WebServer` | no |
| asg_max_size | Maximum size of ASG group. | string | `1` | no |
| asg_min_size | Minimum size of ASG group. | string | `1` | no |
| asg_trigger_breach_duration | Amount of time, in minutes, a metric can be beyond its defined limit before the trigger fires. | string | `5` | no |
| asg_trigger_lower_breach_scale_increment | How many Amazon EC2 instances to remove when performing a scaling activity. | string | `-1` | no |
| asg_trigger_lower_threshold | If the measurement falls below this number for the breach duration, a trigger is fired. | string | `2000000` | no |
| asg_trigger_measure_name | Metric used for your Auto Scaling trigger. | string | `NetworkOut` | no |
| asg_trigger_period | Specifies how frequently Amazon CloudWatch measures the metrics for your trigger. | string | `5` | no |
| asg_trigger_statistic | Statistic the trigger should use, such as Average. | string | `Average` | no |
| asg_trigger_unit | Unit for the trigger measurement, such as Bytes. | string | `Bytes` | no |
| asg_trigger_upper_breach_scale_increment | How many Amazon EC2 instances to add when performing a scaling activity. | string | `1` | no |
| asg_trigger_upper_threshold | If the measurement is higher than this number for the breach duration, a trigger is fired. | string | `6000000` | no |
| customer | Customer name. | string | `` | no |
| ebs_app | EBS App name. | string | - | yes |
| ec2_instance_type | EC2 instance type. | string | - | yes |
| ec2_key_name | SSH Key Name to insert. | string | `` | no |
| elb_connection_draining_enabled | Should connection draining be enabled. | string | `true` | no |
| elb_connection_draining_timeout | Connection draining timeout in seconds. | string | `180` | no |
| elb_ssl_cert | ARN of ceriticate. | string | - | yes |
| environment | Environment name. | string | - | yes |
| healthcheck_url | Application healthcheck URL. | string | `TCP:80` | no |
| http_cidr_egress | CIDR whitelist outbound ELB connectivity. | string | `<list>` | no |
| http_cidr_ingress | CIDR whitelist for 80 port. | string | `<list>` | no |
| logs_delete_on_terminate | Should logs be removed from CloudWatch when environment is terminated. | string | `false` | no |
| logs_retention | CloudWatch logs retention in days. | string | `7` | no |
| logs_stream | Should logs be published in CloudWatch. | string | `false` | no |
| notification_endpoint | Notification endpoint. | string | `` | no |
| project | Project name. | string | `` | no |
| rolling_update_enabled | Should we update in rolling manner. | string | `true` | no |
| rolling_update_type | Rolling update type. | string | `Time` | no |
| separator | Separator to be used in naming. | string | `-` | no |
| ssh_source_restriction | CIDR SSH access whitelist. | string | `0.0.0.0/0` | no |
| vpc_ec2_subnets | Subnets for autoscaling group. | list | - | yes |
| vpc_elb_scheme | internal or external. | string | `` | no |
| vpc_elb_subnets | Subnets for loadbalancer. | list | - | yes |
| vpc_id | VPC id. | string | - | yes |

## Outputs

| Name | Description |
|------|-------------|
| app-fqdn | Application FQDN. |
| role-name | IAM role name. |

Example Usage
----------------

Including an example of how to use this module:

    module "my_project" {
      source             = "git::https://github.com/michalschott/tf-aws-ebs-environment.git?ref=master"
      app                = "MyApp"
      app_solution_stack = "64bit Amazon Linux 2017.03 v2.7.4 running Multi-container Docker 17.03.1-ce (Generic)"
      ebs_app            = "ElasticBeanstalkAppName"
      ec2_instance_type  = "t2.micro"
      elb_ssl_cert       = "arn::...."
      environment        = "MyEnvironmentName"
      vpc_ec2_subnets    = ["private-sub-az1", "private-sub-az2"]
      vpc_elb_subnets    = ["public-sub-az1", "public-sub-az2"]
      vpc_id             = "vpc-1234"
    }

License
-------

MIT

Author Information
------------------

This role was created in 2017 by [Michal Schott](http://github.com/michalschott).
