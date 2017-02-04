## DATSCI Basecamp

The basecamp contains three dockerized application that are external to the dataci
platform. They are base bricks services.
- Rancher, the container manager service
- Cloudbreak, the cloud cluster provisioning service
- Craddle, the goto gateway to the datsci stack

### Install Rancher
https://github.com/rancher/rancher

Just ssh to the basecamp and run the instance below.

`sudo docker run -d --restart=always -p 8080:8080 rancher/server:latest`

### Install Cloudbreak (with cloudbreak-deployer)

http://sequenceiq.com/cloudbreak-docs/latest/

http://sequenceiq.com/cloudbreak-docs/latest/onprem/

You will need to ssh to the Craddle, configure and generate the docker compose for Cloudbreak. Alternatively you can pop an AWS instance will all already setup (`ami-b0b926c3`).

First create a directory and download and install the latest version of the Cloudbreak deployer.

```bash
mkdir cloudbreak-deployer
cd cloudbreak-deployer
wget http://public-repo-1.hortonworks.com/HDP/cloudbreak/cloudbreak-deployer_x.y.z_Linux_x86_64.tgz
tar xvf cloudbreak-deployer_x.y.z_Linux_x86_64.tgz
```

Copy the deployer script to your local bin.

`sudo cp cbd /usr/local/bin/`

Initialize the deployer.

`cbd init`

Create a Profile file with the settings of the deployment.

```
echo export PUBIC_IP=(Public IP of host) > Profile
echo export PRIVATE_IP=(Private IP of host) > Profile
echo export ACCESS_KEY={AWS Master ACCESS_KEY}  > Profile
echo export SECRET_ACCESS_KEY={AWS Master SECRET_ACCESS_KEY}  > Profile
echo export AWS_ROLE_NAME=iam-r-cloudbreak
echo export UAA_DEFAULT_USER_EMAIL=datsci.0x01@gmail.com > Profile
echo export UAA_DEFAULT_USER_PW=cluster4DATCI > Profile
source ./Profile
```

Creates the uaa.yml file that holds the configuration of the identity server used to authenticate users to Cloudbreak.

`cbd login`

Creates the docker-compose.yml file that describes the configuration of all the Docker containers needed for the Cloudbreak deployment.

`cbd generate`

Finally start Cloudbreak!

`cbd start`

#### Other useful `cdb` commands

```
cbd regenerate         - Regenerates the docker-compose.
cbd doctor             - Checks the health of your configuration.
cbd update             - Checks for a newer version of the deployer script
cbd aws generate-role  - Generates an AWS IAM role for Cloudbreak provisioning on AWS
cbd aws show-role      - Show assumers and policies for an AWS role
cbd aws delete-role    - Deletes an AWS IAM role, removes all inline policies
```
