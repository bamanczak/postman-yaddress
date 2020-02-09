# Postman YAddress [![Build Status](https://travis-ci.com/bamanczak/postman-yaddress.svg?branch=master)](https://travis-ci.com/bamanczak/postman-yaddress)
The goal of this project was to implement automated API tests using Postman and to make them run using TravisCI. YAddress was chosen as a sample API for testing.

## How to run tests?

### Using Postman App
In order to run tests using Postman App please make sure you have the app installed: https://www.postman.com/downloads/
Then please follow below steps:
1. Clone this repository
1. Open Postman app
1. Click `import` button at the top of the screen
1. Select the `YAddress.postman_collection.json` file from your local copy of this repository
1. Select the newly created `YAddress` Collection
1. Click on the gear icon at the top right corner in postman
1. Click `import` button
1. Select the `YAddress_Prod.postman_environment.json` and `YAddress.postman_globals.json`
1. Open Postman Runner (`Runner` button at the top of the screen)
1. Select `YAddress` Collection
1. Select `Prod` as environment
1. Click `Start Run`
1. Enjoy the tests

### Using Command line
1. Install npm
1. Install newman
1. Clone this repository
1. Navigate to this repository
1. Execute `newman run YAddress.postman_collection.json -e YAddress_Prod.postman_environment.json -g YAddress.postman_globals.json`

### Using TravisCI
Tests are executed automatically after each commit to this repository. The build definition is stored in `.travis.yml`

## How the postman collection is structured?
### UserKey
UserKey is stored as a global variable. If you wish to use your UserKey in tests, please provide it in the global variables

### URL
URL to YAddress server is stored in the Environment variable (visible in file: YAddress_Prod.postman_environment). If you wish to test using different server please create a new collection environment or change the `baseURL` variable in the environment `Prod`

### Test data
Test data (AddressLine1, AddressLine2 and all details about correct target address, i.e. White House in Washington DC) are stored in the collection variables (visible if you right-click on the collection and click `edit`)

### Reusable scripts
All reusable scripts (like verification of all the details of the address) are defined in the `Pre-requests Scripts` of the Postman collection. Code is saved as environment variable and later on executed in each script using the eval function.

## TODO
1. Increase Test coverage
  1. Define test data for Error Code `5 - Ambiguous street name. More than one street matches the search address with equal accuracy.`
  1. Add tests for all `GeoPrecision` outputs (0-5)
  1. Consider adding more tests for automatic typos and common errors correction
  1. Consider launching tests on a different environment and, if possible how to test error codes related to the server malfunction (1, 6, 7)
1. Consider changing the way reusable scripts are defined: currently in the `Pre-requests Scripts` which causes the code to be executed before every single request.
