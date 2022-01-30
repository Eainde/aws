# Amazon Web Service

## EC2 (Elastic Compute Cloud)

### SSH EC2 instance


1. **ssh -i file.pem username@ip-address**
  - -i: Flag that specifies an alternate identification file to use for public key authentication.
  - username: Username that uses your instance
  - ip-address: IP address given to your instance

eg ssh -i Users/eainde/AD/AWS/EC2Tutorial.pem ec2-user@35.177.57.219 

ec2-user is basically the linux user in the amazon linux machine.

2. If you get the error Unportected private key file or permission to 0644 for 'Ec2Tutorial.pem' are too open.This is beacuse SSH keys are normally used to permit connecting to remote servers without a password. Possession of the private key would permit someone to log into your account on any system which accepts the key. ssh-keygen and the other ssh utilities require private key files to have restricted permissions because the files are sensitive and need to remain secure.
3. To fix the point 2 you have to run below command to secure your pem file.
- chmod 0400 /Users/eainde/AD/AWS/EC2Tutorial.pem

