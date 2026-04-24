# test_Jenkins

DEV 1

## Jenkins


### Credentials


Step 1: Option 1 (recommended): Generate a new SSH key for Jenkins

Do this on your local machine (not on Jenkins):
```
ssh-keygen -t ed25519 -C "jenkins-hpc"
```
#### 


Step 2: Add public key to HPC

Copy the public key to the HPC login node:

Easiest:
ssh-copy-id -i ~/.ssh/id_ed25519.pub hpcuser@hpc-login.example.gov


## Multibranch pipeline


Branch Sources
* Github

* Credentials: user name and password (personal token) 


Check Periodically if not otherwise run

## Check HPC output
