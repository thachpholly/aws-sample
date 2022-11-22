# aws-sample


# Demo 

#Install needed 

## Step 1: Install nodejs 
```
sudo apt update && sudo apt install -y nodejs npm
```

## Create a simple web server
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
