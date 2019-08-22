# Simple test repositories

## Basic Staged Pipeline

        service1:
          fileroot: .
          base: ami-0b898040803850657
          steps:
            - RUN echo $PWD

        service1-deploy:
          fileroot: .
          base: ami-0b898040803850657
          keywords: deploy
          env:
            - APIKEY
          steps:
            - RUN cal
            - RUN ls


## Caching Example

Coming soon (sorry 😔 )

## Windows Example

Coming soon (sorry 😔 )
