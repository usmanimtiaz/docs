
# Automated Tests
Automated Tests directory includes framework for salesforce test automation. It will allow developers to write Scenarios which this framework will run as tests.

## Steps
steps definition comes here

## Configs
- Automated-testing.config.config_service

## Allure Reports
### Not integrated with drone yet
allure_behave: ```behave -f allure_behave.formatter:AllureFormatter -o <path to reports> features/account_page.feature```

## Running Tests locally

### Installing Dependencies
Setup the environment for automated testing by using the requirements-testing.txt

### create a virtual environment and install requirements using pip
* create venv : ```python3 -m venv <path-to-new-virtual-environment>```
* activate venv : ```source <path-to-new-virtual-environment>/bin/activate```
* Install Requirements : ```pip3 install -r requirements-testing.txt```


### Once the Environment is ready go to automated-testing/config/config_service and setup the configuration for your scratch org
- salesforce_app : connected app config
- salesforce_auth : salesforce auth config
- selenium_config : selenium chrome driver path
- salesforce_client : config for making and deleting test data
- For jwt auth to work with your scratch org you will need ssl certificate, you can use a self signed certificate for testing

#### use openssl to create ssl certificate
*  ```openssl genrsa -des3 -passout pass:<randompassword> -out server.pass.key 0000```
*  ```openssl rsa -passin pass:usman -in server.pass.ket -out server.key```
*  ```openssl req -new -key server.key -out server.csr```
*  ```openssl x509 -req -sha256 -days 365 -in server.csr -signkey server.key -out server.crt```

### Run first test
```behave <Automated-testing-dir>/features/account_page.feature```
