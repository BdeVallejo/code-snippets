### Step 1: Download CloudWatch Unified Agent and install it 

```
wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
```
````
sudo rpm -U ./amazon-cloudwatch-agent.rpm
````

### Step 2: Open the configuration panel and set everything up accordingly:

````
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
````

For instance:

    On which OS are you planning to use the agent? : Linux

    Are you using EC2 or On-Premises? : Ec2

    Which user are you planning to run the agent? : root

    Do you want to turn on the StatsD daemon? : No

    Do you want to monitor metrics from CollectD? : No

    Do you want to monitor any host metrics? Yes

    Do you want to monitor CPU metrics per core? Yes

    Do you want to add ec2 dimensions into all of your metrics if the info is available? : Yes

    Would you like to collect your metrics at high resolution? : 1s

    Which default metrics config do you want?: Standard

### Step 3: Start the Agent

```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```
You can check the status by running

````
systemctl status amazon-cloudwatch-agent
````

### End

That´s it. Now you can navigate to CloudWatch and check the metrics under "Metrics => All Metrics => Custom Namspaces".