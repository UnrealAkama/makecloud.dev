# Settings

Makecloud needs a settings file at the root of your project. This won't contain any secrets and can ideally be checked into your code repository with the rest of your code. 

        notify_url: http://localhost:8000/report
        cachable: true
        ignored_files: [ ]
        storage_bucket: makecloud-storage
        aws_security_group: sg-0b1c1099439c1fb2c
        aws_key_name: ecs-key-prod
        aws_subnet_id: subnet-047a9a7a689a05943
