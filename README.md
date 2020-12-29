behave -f allure_behave.formatter:AllureFormatter -o <report-dir> features/account_page.feature


need to authorize the connected app once using following url
https://login.salesforce.com/services/oauth2/authorize?client_id=[client_id]&redirect_uri=[redirect_url]&response_type=code

# Automated Testing
intro

## Features
Test features come here

## Steps
steps definition comes here

## Configs

- AutomatedTesting.config.config_service

## Reports
behave -f allure_behave.formatter:AllureFormatter -o <path to reports> features/account_page.feature

## Running Tests locally
### create a virtual environment and install requirements using pip

```python3 -m venv <path-to-new-virtual-environment>```
```pip3 install -r requirements.txt```

### Once the Environment is ready go to config/config_service and setup the configuration for automated testing

- salesforce_app : connected app config
- salesforce_auth : salesforce auth config
- selenium_config
- salesforce_client : config for making and deleting test data

