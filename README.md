# Automated Tests

This directory includes framework for salesforce tests. It will allow us to write Scenarios which this framework will execute as tests. It uses Behave and Selenium for Behaviour Driven Development.
Behave lets us write tests in natural language and we execute those tests with the help of Selenuim which is an open-source automated testing framework.

Three things to keep in mind while writting tests; Context, Event and Outcome.

- Context is the starting state of our test and is usually denoted by the letter `Given`.
- Envent is what the user does or what we want our test user to do, usually denoted by the letter `When`.
- Outcome is the Expected result we want from our test and is usually denoted by the letter `Then`. 

## Getting Started
Setup the environment for automated testing by using requirements-testing.txt.

- First, create venv `python3 -m venv <path-to-new-virtual-environment>`.
- Activate venv `source <path-to-new-virtual-environment>/bin/activate`.
- Install Requirements `pip3 install -r requirements-testing.txt`.

## Create A Connected App
You'll need refresh_token, offline access for jwt authentication to work.

### Configuration
Once the Environment is ready, go to testing/config/config_service and setup the configuration for your connected App.

- salesforce_app = connected app config
- salesforce_auth = salesforce auth config
- selenium_config = selenium chrome driver config
- salesforce_client = salesforce client that will be used for creating and deleting test data

### use openssl to Generate Certificate
For jwt auth to work with your connected App you will need ssl certificate you can use a self signed certificate for testing.

- `openssl genrsa -des3 -passout pass:<randompassword> -out server.pass.key 0000`
- `openssl rsa -passin pass:<randompassword> -in server.pass.ket -out server.key`
- `openssl req -new -key server.key -out server.csr`
- `openssl x509 -req -sha256 -days 365 -in server.csr -signkey server.key -out server.crt`

Now Upload server.crt to your connected App.

server.key will be used to sign the jwt. Convert server.key to base64 and set env `APP_PRIVATE_KEY`, like `export APP_PRIVATE_KEY=$(cat <path-to-key>/server.key | base64 -w 0)`

## Manually Allow Connected App Access
Allow Connected App access for jwt Authentication. You'll have to be logged-in to Authorize this, which is one of the reasons we can not automate this.
Modify below link as per you connected App.

`https://test.salesforce.com/services/oauth2/authorize?client_id=<CONNECTED_APP_CLIENT_ID>&redirect_uri=<CALLBACK_URL>&response_type=code`

## Run your First Test
To run your first Test `behave testing/features/<feature_name>.feature`

## Write your First Test
Behave operates on directories containing feature and step files. Inside testing directory you'll find features and with in features you'll find steps directory.
Anyone can write scenarios in features file which are linked to steps with `step` decorator.

`Scenario: user navigates to salesforce home page`

To implement this `scenario` we need to open our browser and then goto salesforce login page, enter our credentials and click on login which will take us to salesforce home page. Our scenario alog with steps will be;

```
Scenario: user navigates to salesforce home page
    Given open browser
    Given goto salesforce Login page
    Given enter credentials
    When click on login button
    Then we are at home
```

now we can write steps
