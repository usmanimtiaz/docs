
# Automated Tests
Automated Tests directory includes framework for salesforce test automation. It will allow developers to write Scenarios which this framework will run as tests.

## Steps
steps definition comes here

## Configs
- AutomatedTesting.config.config_service

## Allure Reports
### Not integrated with drone yet
behave -f allure_behave.formatter:AllureFormatter -o <path to reports> features/account_page.feature

## Running Tests locally


### Installing Dependencies
Setup the environment for automated testing by using the requirements-testing.txt

### create a virtual environment and install requirements using pip
* create venv : ```python3 -m venv <path-to-new-virtual-environment>```
* activate venv
* Install Requirements : ```pip3 install -r requirements.txt```


### Once the Environment is ready go to config/config_service and setup the configuration for your scratch org
- salesforce_app : connected app config
- salesforce_auth : salesforce auth config
- selenium_config : selenium chrome driver path
- salesforce_client : config for making and deleting test data

### Run first test
```behave <Automated-testing-dir>/features/account_page.feature```
