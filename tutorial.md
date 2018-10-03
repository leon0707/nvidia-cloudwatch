### Prerequisites:

1. ec2 instance with a Deep Learning AMI.
2. Permission to enable detailed monitoring.

Amazon deep learning ami comes with NVIDIA System Management Interface, so you don't need to install it.

### Enable detailed monitoring
You can enable detailed monitoring on an instance as you launch it or after the instance is running or stopped.

* To enable detailed monitoring for an existing instance using the console
  <img width="462" alt="screen shot 2018-10-03 at 12 03 58 pm" src="https://user-images.githubusercontent.com/523684/46441751-741c3580-c735-11e8-8245-4548ae1ad00d.png">

* To enable detailed monitoring when launching an instance using the console
  <img width="592" alt="screen shot 2018-10-03 at 12 05 46 pm" src="https://user-images.githubusercontent.com/523684/46441779-8bf3b980-c735-11e8-8da7-2590574e05cc.png">

* To enable detailed monitoring for an existing instance using the AWS CLI

  `aws ec2 monitor-instances --instance-ids i-1234567890abcdef0`

* To enable detailed monitoring when launching an instance using the AWS CLI

  `aws ec2 run-instances --image-id ami-09092360 --monitoring Enabled=true...`
  
# Allow instance to push to CloudWatch

Grant your instance the permission to push metrics to Amazon CloudWatch

create policy
<img width="1205" alt="screen shot 2018-10-03 at 1 57 17 pm" src="https://user-images.githubusercontent.com/523684/46441812-a463d400-c735-11e8-9dac-eda6e2152cd4.png">

create role
<img width="975" alt="screen shot 2018-10-03 at 5 57 52 pm" src="https://user-images.githubusercontent.com/523684/46441922-0290b700-c736-11e8-9306-9d8c4ef8252d.png">
<img width="998" alt="screen shot 2018-10-03 at 5 58 31 pm" src="https://user-images.githubusercontent.com/523684/46441921-0290b700-c736-11e8-838e-1a795ceced37.png">
<img width="965" alt="screen shot 2018-10-03 at 5 58 39 pm" src="https://user-images.githubusercontent.com/523684/46441920-0290b700-c736-11e8-9996-4de7796110ab.png">

attach role to instance

<img width="416" alt="screen shot 2018-10-03 at 6 00 34 pm" src="https://user-images.githubusercontent.com/523684/46442003-45528f00-c736-11e8-8083-68200c5822a8.png">

# Clone the repo to your instance
`sudo git clone https://github.com/leon0707/nvidia-cloudwatch.git`

# Install packages
`sudo pip install -r requirements.txt`

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

# Check the result

Go to cloudwatch to check the metrics

<img width="1894" alt="screen shot 2018-10-03 at 4 57 33 pm" src="https://user-images.githubusercontent.com/523684/46442103-93679280-c736-11e8-8765-07ecb0e9973b.png">
<img width="506" alt="screen shot 2018-10-03 at 4 57 46 pm" src="https://user-images.githubusercontent.com/523684/46442104-93679280-c736-11e8-95bc-2b7e320bf608.png">
<img width="1694" alt="screen shot 2018-10-03 at 4 57 56 pm" src="https://user-images.githubusercontent.com/523684/46442247-f35e3900-c736-11e8-8187-03ecc2cdfcc6.png">
<img width="1675" alt="screen shot 2018-10-03 at 4 58 15 pm" src="https://user-images.githubusercontent.com/523684/46442248-f35e3900-c736-11e8-87c9-149b30d01420.png">

# Create alarm
<img width="912" alt="screen shot 2018-10-03 at 5 35 56 pm" src="https://user-images.githubusercontent.com/523684/46442348-564fd000-c737-11e8-8c90-b2c90ab10c2d.png">
<img width="919" alt="screen shot 2018-10-03 at 5 40 20 pm" src="https://user-images.githubusercontent.com/523684/46442349-56e86680-c737-11e8-9925-cd0fbc6a9268.png">


reference: https://aws.amazon.com/blogs/machine-learning/monitoring-gpu-utilization-with-amazon-cloudwatch/
