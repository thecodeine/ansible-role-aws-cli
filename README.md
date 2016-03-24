AWS CLI
=======

An Ansible Role that installs and configures Amazon AWS Command Line
Interface tools on RedHat systems.

Requirements
------------

You will need an Amazon AWS account, with a user and access key security
credentials with permission to the specified bucket.

It is recommended that you create a user with locked down permissions.
Below is a policy named `AmazonS3CreateReadWriteAccess-<bucket-name>`
that can be used to provide limited (create/list/put) access to the
bucket `<bucket-name>`.

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [ "s3:CreateBucket", "s3:ListBucket" ],
                "Resource": [ "arn:aws:s3:::<bucket-name>" ]
            },
            {
                "Effect": "Allow",
                "Action": [ "s3:PutObject" ],
                "Resource": [ "arn:aws:s3:::<bucket-name>/*" ]
            }
        ]
    }

Role Variables
--------------

Available variables are listed below, along with default values (see 
`defaults/main.yml`):

    aws_cli_profile: "default"

For separation we create a new AWS profile for this script context.

    aws_cli_access_key: "<accesss-key>"
    
Your Amazon AWS access key.

    aws_cli_secret_key: "<secret-key>"
    
Your Amazon AWS secret key.

    aws_cli_region: eu-west-1
    
Region name where the S3 bucket is located.

    aws_cli_format: text
    
Output format from the AWS CLI, either `json`, `text` or `table`.

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: mysql-servers
      vars_files:
        - vars/main.yml
      roles:
         - { role: memiah.aws-cli }

*Inside `vars/main.yml`*:

    aws_cli_profile: default
    aws_cli_access_key: "access_key_here"
    aws_cli_secret_key: "secret_key_here"
    aws_cli_region: eu-west-1
    aws_cli_format: text

License
-------

MIT / BSD

Author Information
------------------

This role was created in 2016 by [Memiah Limited](https://github.com/memiah).