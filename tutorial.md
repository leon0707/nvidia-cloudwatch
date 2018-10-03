### Prerequisites:

1. ec2 instance with a Deep Learning AMI.
2. Permission to enable detailed monitoring.

Amazon deep learning ami comes with NVIDIA System Management Interface, so you don't need to install it.

### Enable detailed monitoring
You can enable detailed monitoring on an instance as you launch it or after the instance is running or stopped.

* To enable detailed monitoring for an existing instance using the console

* To enable detailed monitoring when launching an instance using the console

* To enable detailed monitoring for an existing instance using the AWS CLI

  `aws ec2 monitor-instances --instance-ids i-1234567890abcdef0`

* To enable detailed monitoring when launching an instance using the AWS CLI

  `aws ec2 run-instances --image-id ami-09092360 --monitoring Enabled=true...`
  
# Allow instance to push to CloudWatch

Grant your instance the permission to push metrics to Amazon CloudWatch

create policy

create role

attach role to instance

# Clone the repo to your instance
`git clone https://github.com/leon0707/nvidia-cloudwatch.git`

# Install packages
`sudo pip install requirements.txt`

# Update variables in gpumon.py
```python
###CHOOSE NAMESPACE PARMETERS HERE###
my_NameSpace = 'DeepLearningTrain' 

### CHOOSE PUSH INTERVAL ####
sleep_interval = 600

### CHOOSE STORAGE RESOLUTION (BETWEEN 1-60) ####
store_reso = 60
```

# Run script
`python gpumon.py`
