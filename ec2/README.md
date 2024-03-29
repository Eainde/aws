# EC2 (Elastic Compute Cloud)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2.png)


![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_CONFIG.png)


![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_USER_DATA.png)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_Instance_type_overview.png)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_instance_type_general_purpose.png)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_instance_type_compute_optimised.png)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_instance_type_memory_optimised.png)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_instance_type_storage_optimised.png)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_EXAMPLE.png)

## Security Groups


![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/SECURITY_GROUPS.png)


![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/SECURITY_GROUPS_1.png)


![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/PORTS.png)

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
- Savings Plan (1 & 3 years) - commitment to an amount of usage, long workload
- Spot Instances: short workloads, cheap, can lose instances(less reliable)
- Dedicated Hosts: book an entire physical server, control instance placement.
- Dedicated Instances: no other customer will share your hardware
- Capacity Reservations: reserve capacity in a specific AZ for any duration


### EC2 on Demand
- Pay for what you see
   - Linux or Windows - billing per second, after first minute
   - All other operating system- billing per hour
- Has the highest cost but no upfront payment
- No long term commitment
- Recommended for **short term** and **un-interrupted workloads**, where you can't predict how the application will behave

### EC2 Reserved Instances
- Up to 75% discount compared to On-demand
- You reserve a specific instance attributes(Instance Type, region, Tenancy, OS)
- Reservation period: 1 year (+discount) or 3 years(+++ discount)
- Payment options: no upfront(+discount), partial upfront (++discount), All upfront (++discount)
- Reserved Instance's scope - Regional or Zonal(reserve capacity in an AZ)
- Recommended for steady-state usage applications(think database)

##### Convertible Reserved Instance
- Can change the EC2 instance type(e.g. change to t2 large C5 large ), instance family, OS, scope and tenancy
- Up to 66% discount(less discount)

### EC2 Savings Plan
![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_savings_plans.png)

### EC2 Spot Instances
- Can get a discount up to 90% compared to On-demand
- Define max spot price and get the instance while **current spot price < max**
  - The hourly spot price varies based on offer and capacity
  - If a current spot price > your max price you can choose to stop or terminate your instance wait a 2 minutes grace period
- Instances that you can **lose** at any point of time, if your max price is less that the current spot price
- The MOST cost-efficient instances in AWS
- Other Strategy: **Spot Block**
  - "block" spot instance during specified time frame(1 to 6 hours) withour intrruptions
  - In rare situations, the instance may be reclaimed 
  - This is depreciated and will be removed by 31st Dec 2022


- Useful for workloads that are resilient to failure
  - Batch Job
  - Data analysis
  - Image processing
  - Any distributed workloads
  - Workloads wita a flexible start and end time


- Not suitable for critical jobs or databases


![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/terminate_spot_Instances.png)

#### Spot Fleets
- Spot Fleets = set of Spot Instances + (optional) On-Demand Instances
- The Spot Fleet will try to meet the target capacity with price constraints
  - Define possible launch pools: instance type(m5.large), OS, Availability Zone
  - Can have multiple launch pools, so that the fleet can choose
  - Spot Fleet stops launching instances when reaching capacity or max cost
- Strategies to allocate Spot Instances:
  - **lowest price**: from the pool with the lowest price(cost optimization, short workload)
  - **diversified** : distributed accross all pools (great for availability, long workloads)
  - **capacityOptimized**: pool with the optimal capacity for the number of instances
- **Spot Fleets allow us to automatically request Spot Instances with the lowest price**

### EC2 Dedicated Hosts
- An Amazon EC2 Dedicated Hosts is a physical server with EC2 instance capacity fully dedicated to your use. 
- Dedicated Hosts can help you address **compliance requirements** and reduce costs by allowing you to **use your existing server-bound software licenses**
- Purchasing Option:
  - On demand - pay per second for active dedicated host
  - Reserved- 1 or 3 years(No upfront, partial upfront, All upfront)
- The most expensive option

- Useful for software that have complicated licensing model(BYOL- Bring your Own License)
- Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances
- Instances running on hardware that's dedicated to you
- May share hardware with other instance in same account
- No control over instance placement(can move hardware after Stop/Start)

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2_dedicated_instances.png)

**Price Comparison** 

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/PRICE_COMPARISON.png)

### EC2 Capacity Reservations
![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/EC2-CAPACITY-RESERVATIONS.png)

### Which purchasing option right for you?

![](https://github.com/Eainde/aws/blob/main/ec2/src/main/resources/WHICH-IS-RIGHT-FOR-ME.png)




