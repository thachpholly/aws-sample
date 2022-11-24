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
