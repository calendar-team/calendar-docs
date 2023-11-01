# Deploy `calendar-backend` to EC2

Currently, the `calendar-backend` is deployed to EC2.

This guide will describe how to deploy on a new EC2 machine and how to configure the deployment pipeline.

1. First we need to launch a new EC2 instance
   ![new_ec2_instance_for_backend.png](./images/new_ec2_instance_for_backend.png)
    1. Choose `Amazon Linux` as OS and a 64 bit architecture
       ![new_ec2_instance_for_backend_os.png](./images/new_ec2_instance_for_backend_os.png)
    2. Instance type: `t2.nano`
       ![new_ec2_instance_for_backend_type.png](./images/new_ec2_instance_for_backend_type.png)
       This is the cheapest and smallest instance type.
    3. Choose `calendar-backend` as the key pair
       ![new_ec2_instance_for_backend_key_pair.png](./images/new_ec2_instance_for_backend_key_pair.png)
       Or we can create a new key pair, just make sure to update the github secret (details will follow in a step below).
    4. Use `calendar-backend` security group
       ![new_ec2_instance_for_backend_sg.png](./images/new_ec2_instance_for_backend_sg.png)
       Or we can create a new security group, we will need the following ports to be added under the inbound rules:
       - `22` - `SSH` port used by [our github-actions](https://github.com/calendar-team/calendar-backend/blob/master/.github/workflows/deploy_on_ec2.yml) workflow to deploy new version of `calendar-backend`
       - `443` - used by certbot to renew the TLS certificate (details will follow in a step below)
       - `8080` - this is the port that `calendar-backend` uses
    5. Allocate a 30 GB gp3 disk
       ![new_ec2_instance_for_backend_disk.png](./images/new_ec2_instance_for_backend_disk.png)
2. Configure the TLS certificate by following the tutorial from [here](https://certbot.eff.org/instructions?ws=other&os=pip). 
   
   Note that you will have to `ssh` into the EC2 machine for setting the certificate. To do this we will need:
   - the private key from the key pair that we chose on instance creation from above
   - the public DNS of our EC2 instance. This can be found in AWS console on instance details
   - run the following command from a terminal:
     ```
     ssh -i PATH_TO_SSH_KEY ec2-user@EC2_PUBLIC_DNS
     ```

   Also make sure that the `calendar-backend` is [pointing](https://github.com/calendar-team/calendar-backend/blob/master/src/lib.rs#L308-L313) to the correct certificate.
3. Configure the deployment pipeline. For this we will have to update a few github secrets:
   - [SSH_PRIVATE_KEY](https://github.com/calendar-team/calendar-backend/settings/secrets/actions/SSH_PRIVATE_KEY) - this should be the private key of the key pair configured on EC2 from above
   - [REMOTE_HOST](https://github.com/calendar-team/calendar-backend/settings/secrets/actions/REMOTE_HOST) - this should be the public DNS of our EC2 instance
   - [REMOTE_USER](https://github.com/calendar-team/calendar-backend/settings/secrets/actions/REMOTE_USER) - set this to `ec2-user`
   - [CALENDAR_JWT_SIGNING_KEY](https://github.com/calendar-team/calendar-backend/settings/secrets/actions/CALENDAR_JWT_SIGNING_KEY) - the secret key used by the `calendar-backend` to sign jwt tokens
4. Finally we can trigger `Deploy to EC2` workflow to deploy `calendar-backend` to the newly created EC2 instance

You can find a sequence diagram explaining the process of deploying to EC2 [here](./decisions/0001-calendar-backend-ci-cd.md#github-actions-with-ssh-and-rsync).
