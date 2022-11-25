# AWS cloudwatch

This section will demostrate how to config cloudwatch

## Install cloudwatch agent

```
wget https://s3.amazonaws.com/amazoncloudwatch-agent/ubuntu/amd64/latest/amazon-cloudwatch-agent.deb
```
```
sudo dpkg -i -E ./amazon-cloudwatch-agent.deb
```

## Configuration cloudwatch agent

```
sudo vim /opt/aws/amazon-cloudwatch-agent/bin/config.json
```

 ```
 {
     "agent": {
         "run_as_user": "root"
     },
     "logs": {
         "logs_collected": {
             "files": {
                 "collect_list": [
                     {
                         "file_path": "/var/log/apache2/error.log",
                         "log_group_name": "apache-log",
                         "log_stream_name": "{instance_id}"
                     },
                     {
                         "file_path": "/var/log/apache2/access.log",
                         "log_group_name": "apache-log",
                         "log_stream_name": "{instance_id}"
                     }
                 ]
             }
         }
     }
 }
 ```

## Start run collect log
```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

## Open cloudwatch to see results

### Option 1 : AWS Console
[cloudwatch](https://ap-southeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-southeast-1#logsV2:log-groups/log-group/apache-log)

### Option 2 : AWS toolkit

Eclipse: [Eclipse plugin](https://aws.amazon.com/vi/eclipse/)

Intellij: [Intellij plugin](https://aws.amazon.com/intellij/)

VScode: [VScode plugin]([https://aws.amazon.com/intellij/](https://aws.amazon.com/visualstudiocode/))

### Option 3 : AWS CLI
Start a query then it return a query-id
```
aws logs start-query --start-time 1669039558 --end-time 1669339558 --log-group-name apache-log --query-string  "error"
```
Get result by query-id
```
aws logs get-query-results --query-id 3b53e535-5d10-4eb6-8a98-5994cc5b4a05
```
