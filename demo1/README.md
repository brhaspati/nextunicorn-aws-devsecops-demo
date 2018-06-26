# AWS Workshop:  `DevSecOps - Building secure applications in AWS`

# Objective
Provide hands on experience in using AWS services to secure your internet facing applications.

# Demo 1

## Design goes here

## Setup instructions

### Step 1: Pre-requisites
* Login to your AWS Console
* Go to IAM and make sure your IAM user has administrator policy attached. This will help to run these demos without any issues.

<img width="1372" alt="IAM Administrator rights needed" 
src="http://devsecops-demo-images.s3-website-eu-west-1.amazonaws.com/Screen%20Shot%202018-06-26%20at%2016.14.00.png">


* Select region as "EU-WEST-1". We have hard corded all the configurations to point to EU-WEST-1 to simplify the setup of the demo. 
It will not work or will give misleading error if you attempt to run some of the Cloudformation templates in another region.

### Step 2: Setting up S3 for website hosting
* Go to `S3` service and click `Create Bucket` button <br>
   * In the pop-up window give an unique name for your bucket. <br>
   * Make sure you choose, EU-WEST-1 as the region <br>
   * Click next and next to complete the setup. <br>
* Click the new bucket and go to the properties<br>
<img width="1372" alt="S3 properties" 
src="http://devsecops-demo-images.s3-website-eu-west-1.amazonaws.com/Screen%20Shot%202018-06-26%20at%2016.26.33.png">
* Select the `Static Web Hosting` option and fill in the details as below
<img width="1372" alt="S3 enable static hosting" 
src= "http://devsecops-demo-images.s3-website-eu-west-1.amazonaws.com/Screen%20Shot%202018-06-26%20at%2016.26.58.png">


### Step 3: Run the cloudformations templates to setup the demo1

* Go to `CloudFormation` service


* Click `Create Stack` Button
<img width="1372" alt="Cloudformation" 
src="http://devsecops-demo-images.s3-website-eu-west-1.amazonaws.com/Screen%20Shot%202018-06-26%20at%2016.15.48.png">

* Choose `Upload a template to S3` option and use the file selector to choose `1-setup-myunicorn-app.json` and click `Next` Button

<img width="1372" alt="Upload the cloudformation json" 
src="http://devsecops-demo-images.s3-website-eu-west-1.amazonaws.com/Screen%20Shot%202018-06-26%20at%2016.17.43.png">

* Fill in the details for the cloudformation<br><br>
  * `Stack Name` text box provide a name to your stack `nextunicorn-app`<br><br>
  * `Website Bucket` text box provide the name of the bucket you created in Step 2 and click `Next` Button
<img width="1372" alt="provide website bucket name" 
src="http://devsecops-demo-images.s3-website-eu-west-1.amazonaws.com/Screen%20Shot%202018-06-26%20at%2016.32.03.png">


* All the fields in this screen are option, just click `Next` Button
<img width="1372" alt="next screen" 
src="https://s3-eu-west-1.amazonaws.com/devsecops-demo-images/Screen+Shot+2018-06-26+at+16.32.24.png">

* Make sure you select the `tick box` to *Acknowledge* you give neccessary permission to create the resources and click `Create` Button

<img width="1372" alt="final screen" 
src="https://s3-eu-west-1.amazonaws.com/devsecops-demo-images/Screen+Shot+2018-06-26+at+16.32.38.png">

* Wait for the stack to be created
* Once the stack creation is complete, click the `output` tab to get your `ServiceEndPoint` URL. You will need this for subsequent steps
<img alt="Service Endpoint details" src="https://s3-eu-west-1.amazonaws.com/devsecops-demo-images/Screen+Shot+2018-06-26+at+16.38.35.png">

### Step 4: Slack incomming webhook


### Step 5: Update the Front end and upload
* Go to `demo1/frontend/src` directory
* Open `functions.js` and update the first line<br>
var URL with your `ServiceEndPoint` URL.<br>
```javascript
var URL = "https://yourserviceendpoint/dev"
```
<img alt="update the var"
src="https://s3-eu-west-1.amazonaws.com/devsecops-demo-images/Screen+Shot+2018-06-26+at+16.45.55.png">

* Open `notifications-config.json`

```javascript
 "alert": {
                "slack": {
                        "enabled": "true",
                        "webhook-url": "https://hooks.slack.com/services/XXXXXX/YYY/YOURWEBHOOK"
                },
```

* Copy the files to the website S3 bucket


### Step 6: Verify the installation

#### Testing honeyLambda
Go to the browser and type the URL with
```javascript
https://o8qqpwhy5d.execute-api.eu-west-1.amazonaws.com/dev/v1/get-pass
```

You will get following message when everything is setup correctly
<img alt="Honey pot is working"
src="https://s3-eu-west-1.amazonaws.com/devsecops-demo-images/Screen+Shot+2018-06-26+at+16.56.51.png">

or 

You will get internal server error.
<img alt="internal server error" src="https://s3-eu-west-1.amazonaws.com/devsecops-demo-images/Screen+Shot+2018-06-26+at+16.49.30.png">
Make sure you have copied the `notifications-config.json` to your website bucket.






