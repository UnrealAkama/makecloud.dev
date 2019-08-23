# Getting Started

## Setting up AWS

This section assumes some familarity with AWS and concepts & terms related to it.

The setup required for Makecloud involves setting up a ssh key, a security group, a subnet inside a vpc and a storage bucket for the cache.

### SSH Key

Generate or take an existing key and upload it to AWS. Note the pair name for putting in the mc_settings.yaml file later.

### Subnet

You can create a new VPC for Makecloud or use an existing one. If you use an existing one, it's strongly recommended that you create a seperate subnet for the Makecloud nodes. Note the name for mc_settings.yaml later.

### Security Group

In the same vpc as your subnet, create a new security group and only allow ports 22, 8000 inbound from the internet. Port 22 is secured by a ssh key and port 8000 is secured by a key that is provided by Makecloud when the box is started. Please note this security group for the mc_settings.yaml file.

### S3 Bucket

Make a new bucket with a name of your choice. It's highly recommended that you turn on object expiration, Makecloud expects that objects disappear over time and will handle that gracefully by rebuilding the cache'd object if it's still needed. The developers currently use it with a expiration time of 30 days and that seems like a nice balance between keep cache'd states for a bit and reducing storage costs.

## Setting up your first Makecloud run

There are two major pieces to enabling Makecloud support in a project. At the root of your project, you will need to place a mc_settings.yaml file. You can find the reference for that [here](/docs/settings/). Fill in the values for the AWS objects above into that file. Feel free to ignore the `notify_url` at the moment, that only matters if you want your CLI runs to report builds to a central build server. `ignored_files` should be filled in with any files that don't need to be uploaded to your worker nodes. In OCaml using dune and opam with local switches, you probably want to add `_opam` and `_build` to it at the minimum.

You are now ready to write your first node. Node definitions can be placed in any folder in your project as long as the file is called `makecloud.yaml`. It's recommend for them to live close to the code they are building and testing. It's recommend that as a start, you try placing the following nodes in a file called `makecloud.yaml` in the same folder as the settings file called `mc_settings.yaml`.

        first-stage:
          fileroot: .
          base: ami-0b898040803850657
          steps:
            - RUN datetime

        second-stage:
          fileroot: .
          base: ami-0b898040803850657
          dependson:
            - first-stage
          steps:
            - RUN datetime

You can now run `mc invoke` and you should see the node spinning up and running the datetime command. Once the first node is done, you will see a second node spin up and run it's datetime command. You can now write Makecloud nodes. You can find more information about how to write more complex nodes [here](/docs/node_definition/). Congratulations and have a hopefully happy time using Makecloud.
