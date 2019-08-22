# Settings

Makecloud needs a settings file at the root of your project. This won't contain any secrets and can ideally be checked into your code repository with the rest of your code. The one below can serve as a basic example for what a simple file looks like.

        notify_url: http://localhost:8000/report
        cachable: true
        ignored_files: [ ]
        storage_bucket: makecloud-storage
        aws_security_group: sg-0b1c1099439c1fb2c
        aws_key_name: ecs-key-prod
        aws_subnet_id: subnet-047a9a7a689a05943

## notify_url

`notify_url` is used to configure which web server that the command line tool should notify and keep informed of a build's progress.

## cachable

`cachable` is used to configure caching, setting it to false will disable caching for the project as a whole.

## ignored_files

`ignored_files` is used to ignore certain processing of files. It won't transfer these files to the VM running the worker node.

## storage_bucket

`storage_bucket` controls the name of the S3 bucket that will be used to store the cache, stored logs for runs, and transfering files. The AWS credentials that Makecloud uses must have access to list objects, get objects, and put objects.

## aws_security_group

`aws_security_group` is the name of the AWS security group for EC2. This security group must have TCP access to port 8080.

## aws_key_name 

`aws_key_name` is the name of the ssh key that will be installed on the box. This isn't actually used in the operation of Makecloud but can be used to debug failed nodes.

## aws_subnet_id 

`aws_subnet_id` is the subnet in AWS that you wish for nodes to be located in. For security reasons, it's recommended that this is seperated from other running systems.
