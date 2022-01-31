# EC2 (Elastic Compute Cloud)

## SSH EC2 instance

```shell
ssh -i file.pem username@ip-address
```
  - -i: Flag that specifies an alternate identification file to use for public key authentication.
  - username: Username that uses your instance
  - ip-address: IP address given to your instance

eg.
```shell
ssh -i Users/eainde/AD/AWS/EC2Tutorial.pem ec2-user@35.177.57.219 
```
ec2-user is basically the linux user in the amazon linux machine.

<br /> If you get the error Unprotected private key file or permission to 0644 for 'Ec2Tutorial.pem' are too open.This is beacuse SSH keys are normally used to permit connecting to remote servers without a password. Possession of the private key would permit someone to log into your account on any system which accepts the key. ssh-keygen and the other ssh utilities require private key files to have restricted permissions because the files are sensitive and need to remain secure.
<br /><br /> To fix the above point you have to run below command to secure your pem file. <br />

```shell
chmod 0400 /Users/eainde/AD/AWS/EC2Tutorial.pem
```

## EC2 Instances Purchasing Options
- On-Demand Instances: short workload, predictable pricing
- Reserved: (Minimum 1 year)
  - Reserved Instance: long workloads
  - Convertible Reserved Instances: long workloads with flexible instances
  - Schedule Reserved Instances: example - every Thursday between 3 and 6 pm
- Spot Instances: short workloads, cheap, can lose instances(less reliable)
- Dedicated Hosts: book an entire physical server, control instance placement.


### EC2 on Demand
- Pay for what you see
   - Linux or Windows - billing per second, after first minute
   - All other operating system- billing per hour
- Has the highest cost but no upfront payment
- No long term commitment
- Recommended for short term and un-interrupted workloads, where you can't predict how the application will behave

### EC2 Reserved Instances
- Up to 75% discount compared to On-demand
- Reservation period: | year = + discount | 3 years = +++ discount
- Purchasing options: no upfront | partial upfront = + discount | All upfront = ++ discount
- Reserve a specific instance type eg large
- Recommended for steady-state usage applications(think database)

##### Convertible Reserved Instance
- Can change the EC2 instance type(eg. change to t2 large C5 large )
- Up to 54% discount(less discount)

##### Scheduled Reserved Instances
- launch within time window you reserve
- When you require a fraction of day/ week / month
- Still commitment over 1 to 3 years

### EC2 Spot Instances
- Can get a discount up to 90% compared to On-demand
- Instances that you can **lose** at any point of time, if your max price is less that the current spot price
- If a current spot price > your max price you can choose to stop or terminate your instance wait a 2 minutes grace period
- The MOST cost-efficient instances in AWS


-Useful for workloads that are resilient to failure
  - Batch Job
  - Data analysis
  - Image processing
  - Any distributed workloads
  - Workloads wita a flexible start and end time


- Not suitable for critical jobs or databases


![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/terminate_spot_Instances.png)

### EC2 Dedicated Hosts
- An Amazon EC2 Dedicated Hosts is a physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts can help you
address **compliance requirements** and reduce costs by allowing you to **use your existing server-bound software licenses**
- Allocated for your account for a 3-year period reservation
- More expensive

- Useful for software that have complicated licensing model(BYOL- Bring your Own License)
- Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances
- Instances running on hardware that's dedicated to you
- May share hardware with other instance in same account
- No control over instance placement(can move hardware after Stop/Start)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_dedicated_instances.png)

**Price Comparison** 


![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/PRICE_COMPARISON.png)




