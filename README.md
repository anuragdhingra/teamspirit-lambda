# teamspirit-lambda
AWS lambda functions to clock-in/clock-out from [teamspirit](https://www.teamspirit.com/) deployed via Serverless framework

### Install
Go to root directory of project
```buildoutcfg
# download Selenium 2.37
$ pip3.6 install -t layers/seleniumLayer/selenium/python/lib/python3.6/site-packages selenium==2.37

# download chrome driver
$ cd layers/seleniumLayer
$ mkdir chromedriver
$ cd chromedriver
$ curl -SL https://chromedriver.storage.googleapis.com/2.37/chromedriver_linux64.zip > chromedriver.zip
$ unzip chromedriver.zip
$ rm chromedriver.zip

# download chrome binary
$ curl -SL https://github.com/adieuadieu/serverless-chrome/releases/download/v1.0.0-41/stable-headless-chromium-amazonlinux-2017-03.zip > headless-chromium.zip
$ unzip headless-chromium.zip
$ rm headless-chromium.zip

```

### Install serverless command
Do this if you don't have serverless in your machine yet
```Try running,
npm config set prefix /usr/local
and then,
npm i -g serverless
```

### Deploy Lambda Layers for selenium and chrome driver
Go to root directory of project
```buildoutcfg
$ cd layers
$ sls deploy 
```

### Create config file and set teamspirit credentials
Go to root directory of project
```buildoutcfg
$ cd lambda
$ cp config.dev.json.example config.dev.json 
```
Edit `config.dev.json` file and set your teamspirit credentails. <br>
*Note: These credentials would be stored as enviroment variables for lambda functions. Alternatively, you could use Paramter store or Secrets Manager to store them. More details [here](https://serverless-stack.com/chapters/storing-secrets-in-serverless-apps.html)*

### Deploy clock_in and clock_out Lambda Functions
Go to root directory of project
```buildoutcfg
$ cd lambda
$ sls deploy 
```

### Start Testing 
Check serverless logs or log into AWS console navigate to API gateway to find generated API endpoints(/clockIn and /clockOut) 
Or, you could invoke lambdas directly
```buildoutcfg
$ cd lambda
$ sls invoke --function teamspirit-lambda-dev-clock_in
$ sls invoke --function teamspirit-lambda-dev-clock_out
```

### Additional Usecases
The generated API endpoints could be triggered via google assistant as well by creating a custom google action, connecting it with a dialogue flow agent and adding the API endpoints(clockIn/clockOut) as webhooks in the fulfillment section. [Example](https://codelabs.developers.google.com/codelabs/actions-1/?hl=ja#0).
