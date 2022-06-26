
![placeholder image](https://camo.githubusercontent.com/3e4803b1e1707d4eb08aafb50318f23658ea195438834b840a2f393a9b9edba4/68747470733a2f2f6b61736d2d7374617469632d636f6e74656e742e73332e616d617a6f6e6177732e636f6d2f6c6f676f5f6b61736d2e706e67)

# Kasm Workspaces Streams Dockerized Apps in the Browser

## Introduction

Tried to run docker-apps through kasm workspace, using Linode Cloud.
Any other cloud service provider with VM support can also be used. (AWS, Azure, GCP, IBM Cloud, DigitalOcean)

## Use Case

- Provides Separate space to work in
- Privacy
- Multi-user support
- Remote access through IP
- SSH access from desktop terminal

## Cloud Research

- I spun Ubuntu 20.4 LTS over Linode (4 Gigs RAM, Shared 2 core CPU Configuration)
- Terminal access through ssh root@[linode-ip-address]
- Swap Configuration using the following commands

```
sudo dd if=/dev/zero bs=1M count=1024 of=/mnt/1GiB.swap

sudo chmod 600 /mnt/1GiB.swap

sudo mkswap /mnt/1GiB.swap

sudo swapon /mnt/1GiB.swap

```

- Checks if the swap is done correctly
```
cat /proc/swaps

```
- Checks if the swap exists after Reboot of the instance

```
echo '/mnt/1GiB.swap swap swap defaults 0 0' | sudo tee -a /etc/fstab

```
- Install KASM
```
wget https://kasm-static-content.s3.amazonaws.com/kasm_release_1.10.0.238225.tar.gz

tar -xf kasm_release*.tar.gz

sudo bash kasm_release/install.sh

```

- After the entire process, The credentials will be displayed in the Terminal window. Copy and paste to store them in a safe place, for future use.
- Finally, open any browser (Recommended : Safari) and type the URL as, https://[your-linode-ip]

## Social Proof

<img width="1133" alt="Screenshot 2022-06-26 at 9 12 16 PM" src="https://user-images.githubusercontent.com/91361382/175822273-81030d32-577e-4d3d-bbc1-02be671796ef.png">


