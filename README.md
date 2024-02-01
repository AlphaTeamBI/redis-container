Redis container image - AlphaTeam
=================================

We forked this repo from : [scolrg](https://github.com/sclorg/redis-container/)

On this repository we made some changes on redis 7 version in order to add more settings on the redis.conf file. 
We edited files in ./7/root/usr

Create Image
------------

To build a Redis image, choose either the CentOS or RHEL based image:
*  **RHEL based image**

    We chose to create RHEL image for example so we will create the image from the matching DockerFile: Dockerfile.rhel9.

    First enter the folder of redis version you want to use:

    ```
     cd ./7
    ```
    * Before running, make sure all files in this folder set to LF (End of line sequence) 

    Now, you can create the image

    ```
     docker build -t redis:7-el9 -f ./Dockerfile.rhel9 .
    ```

Use Image in Deployment
-----------------------
Now you can use the image you created as the image of your redis service in openshift.

You can inject the followings environment variables in DeploymentConfig in order add redis.conf settings:

```
    # Password for default user (recommanded)
    REDIS_PASSWORD 

    # Set acl user - this user can use replicaof method and does not have full access to Redis instance (recommanded)

    REPLICA_USER
    REPLICA_USER_PASSWORD

    # # Set current redis instance as replicaof another redis instance if master props are defined (optional)

    REDIS_REPLICA_MODE ("ON" / "OFF")

    # Variables you have to define if you set REDIS_REPLICA_MODE="ON"

    REDIS_MASTER_IP
    REDIS_MASTER_PORT
    REDIS_MASTER_PASSWORD
```