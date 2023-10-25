# How to deploy to EC2

Currently, the `calendar-backend` is deployed to EC2.

This guide will describe how to deploy on a new EC2 machine and how to configure the deploy pipeline.

1. Launch a new EC2 machine
    1. Choose `Amazon Linux` as OS and a 64 bit architecture
    2. Instance type: `t2.nano`
    3. Choose `calendar-backend` as the key pair
    4. Use `launch-wizard-3` security group
    5. Allocate a 30 GB gp3 disk
2. Configure the TLS certificate by following the tutorial from [here](https://certbot.eff.org/instructions?ws=other&os=pip). Also make sure that the `calendar-backend` is [pointing](https://github.com/calendar-team/calendar-backend/blob/master/src/lib.rs#L308-L313) to correct certificate.
3. Configure the Github secrets. Just make sure that the correct secret is added under `SSH_PRIVATE_KEY`, it should be the same key as the one configured on EC2.
4. Trigger a deployment
