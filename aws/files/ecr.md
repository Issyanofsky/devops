<div align="center">

# **Elastic Container Registry (ECR)**

</div>

 fully managed container image registry service provided by AWS (like DockerHub).

 # Create an ECR Repository

     Navigate to the ECR webpage.

     --> create repository

          choose between a public or private repository:

              - A public repository is accessible to everyone.
              - A private repository is restricted to users with permissions.

        Mutable - allow overwrite Images.
        Immutable - no allow overwrite images (dont declair "Latest" )

        Image security - scan the image.

        --> create

  # upload an Image

  using gitbash:

      after connecting to the right region.

      use the Push command showed on the repo. 
            
