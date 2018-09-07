Referencing bugreport: https://github.com/serverless/serverless/issues/5278

## Steps to repoduce

1. `npm i`
2. `npm run sls:deploy`

The output is:

```
$ npm run sls:deploy

> sls-test@1.0.0 sls:deploy /test-folder/sls-deploy
> SLS_DEBUG=true sls deploy

Serverless: Load command config
Serverless: Load command config:credentials
Serverless: Load command create
Serverless: Load command install
Serverless: Load command package
Serverless: Load command deploy
Serverless: Load command deploy:function
Serverless: Load command deploy:list
Serverless: Load command deploy:list:functions
Serverless: Load command invoke
Serverless: Load command invoke:local
Serverless: Load command info
Serverless: Load command logs
Serverless: Load command login
Serverless: Load command logout
Serverless: Load command metrics
Serverless: Load command print
Serverless: Load command remove
Serverless: Load command rollback
Serverless: Load command rollback:function
Serverless: Load command slstats
Serverless: Load command plugin
Serverless: Load command plugin
Serverless: Load command plugin:install
Serverless: Load command plugin
Serverless: Load command plugin:uninstall
Serverless: Load command plugin
Serverless: Load command plugin:list
Serverless: Load command plugin
Serverless: Load command plugin:search
Serverless: Load command config
Serverless: Load command config:credentials
Serverless: Invoke deploy
Serverless: Invoke package
Serverless: Packaging service...
Serverless: Excluding development dependencies...

$ 
```

After which it silently stops without deploying.

In `serverless.yml` you can uncomment `provider.name` to `aws` and it will work fine.

`sls print` will print a correct `serverless.yml` file with and without the file import.

```
$ sls print
service: sls-deploy-test
provider:
  stage: dev
  region: eu-west-1
  name: aws
  runtime: nodejs8.10
functions:
  onlyDatHuisEmail:
    handler: ./index.handler
    memorySize: 128
    timeout: 3

```
