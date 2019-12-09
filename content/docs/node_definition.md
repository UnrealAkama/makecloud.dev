# Writing a Node Definition

Here is an example node definition:

        serviceA-deploy:
          fileroot: serviceA
          base: ami-0b898040803850657
          keywords: deploy
          env:
            - APIKEY
          steps:
            - RUN cal
            - RUN ls

Node definitions are written in Yaml with a single block describing a whole node. The name of the node is what all other attributes of the node are filled under.

## fileroot

The fileroot parameter is used to control caching for the individual folder or file relating to building a service. It is relative to the root of the project as a whole. This can also take a list of file roots or specific files to hash.

## base

Right now with only one provider, this is simply the AMI id that the node should run under. In the future, this is likely to be a provider specific setting.

## keywords

`deploy` marks a node that should only run when the deploy flag is provided.

`windows` marks a node as having to use the windows agent and init script instead of the Linux one.

## env

Any argument listed under here will be taken from the system where Makecloud was invoked and passed onto the virtual machine running the agent. This is frequently useful for security credentials or other items that you don't want to commit into the codebase.

## steps

This is a series of steps or commands that gets executed on the node.

`RUN` Executes the command in bash on linux or for powershell on windows

`UPLOAD` Uploads a file from the virtual machine into s3. It takes two arguements, the first of which is an absolute path and the second being a unique name per stage to identify the storage.

`DOWNLOAD` Downloads a file that was uploaded by another stage. It takes two arguments, the first is the name of the node and the file to retrieve from it in the form of node_name/file_name. The second is an absolute path where to store the file on a Linux system.
