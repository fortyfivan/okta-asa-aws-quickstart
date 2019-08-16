# Okta Advanced Server Access AWS Quick Start

This Quick Start deploys a sample bastion architecture backed by Okta Advanced Server Access. It deploys a VPC with a public and private subnet, a bastion host, and a target instance. The Okta Advanced Server Access server agent is installed on both EC2 instances, which delivers a Zero Trust mechanism to authenticate using SSH Client Certificates via an Okta Identity-led authentication workflow.

![Okta Advanced Server Access Quick Start Architecture](https://github.com/fortyfivan/okta-asa-aws-quickstart/blob/master/okta-asa-quick-start-architecture.png)

The following instructions require an Okta tenant with Administrative rights. If you do not have an Okta tenant, sign up for a free trial at https://www.okta.com/free-trial.

## Create an Advanced Server Access team:

1. Sign up for Advanced Server Access at https://app.scaleft.com/p/signup
2. Follow the workflow to integrate with your Okta Org
3. Download the Client Application at: https://help.okta.com/en/prod/Content/Topics/Adv_Server_Access/docs/setup/enrolling-a-client.htm
4. Create a Project and assign a Group that includes users you wish to grant access
5. Generate an Enrollment Token (copy this value, you will use it in the CloudFormation template) 

## Deploy the CloudFormation template:

1. Sign up for an AWS account at https://aws.amazon.com, select a region, and create a key pair for the bastion host and for the target instance.
2. In the AWS CloudFormation console, launch the template to build a new stack. Choose the parameters, and paste the Enrollment Token for the Advanced Server Access project you wish to enroll the instances with
3. When deployed, confirm that the instances were properly enrolled by visiting the Advanced Server Access dashboard
4. Use the CLI to login to the newly deployed target instance via the bastion by running `sft ssh <target-instance>`

* Optionally, you can configure ProxyCommand for your local SSH to avoid having to preface ssh commands with sft. Run `sft ssh-config` and copy the output to your local SSH configuration *