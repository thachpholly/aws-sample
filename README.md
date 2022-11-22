# aws-sample
This demo will demonstate how we can use AWS to create a webserver.


# Create EC2 Instance
  ## Option 1:
  Use AWS CLI
  ```
   aws ec2 run-instances ...
  ```
  ## Option 2;
   Use AWS Console create a new instance
   https://ap-southeast-1.console.aws.amazon.com/ec2/home?region=ap-southeast-1#Instances


# Connect to EC2 Instance do follow below steps


## Step 1: Install nodejs & expressjs
```
sudo apt update && sudo apt install -y nodejs npm
```
```
npm install express
```

## Step 2: Create a simple web server
```
nano app.js
```

```
const express = require('express')
const app = express()
const port = 3000
app.get('/', (req, res) => {
  res.send('Hello World!')
})
app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

## Step 3: Run It
```
node app.js
```

# Test It

Go to http://replace_with_your_ec2_public_ip:3000

