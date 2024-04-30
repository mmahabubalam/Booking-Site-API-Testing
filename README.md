
# Booking Site API Testing with Postman Newman

This is an API testing project using Postman, Given a step by step instruction.

### Feature 
- Tests for POST, GET, PUT, DELETE requests
- Validates different API(s)
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

### API Documentation 
- https://documenter.getpostman.com/view/13082503/2sA2xmUAJ1

### Tools Used
- Postman
- Newman
### Prerequisite:
- Node Js
- Newman
- Newman Html Report Library
### Installation
1. Postman: Download and install Postman.(If you don't have it) [download and install Postman.](https://www.postman.com/downloads/) 

2. Clone the repository: 
```bash
git Clone https://github.com/mmahabubalam/Booking-Site-API-Testing.git
```
3. Import the Postman collection:
- Open Postman.
- Click on the Import button.
- Select the file from the Collection folder of repository.

4. Import the Postman environment:
- In Postman, click on the gear icon in the top right corner.
- Select Import and choose the file.

5. Newman and Report Installation Process:
- Newman Install Command:
```bash
 npm install -g newman
```
- Newman Html Report Install Command:
```bash
npm install -g newman-reporter-htmlextra
```

### Usage
1. Select Environment:
- In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2. Run Collection:
- Select the imported collection from the Collections sidebar.
- Click on the Runner button to open the collection runner.
- Select the desired environment.
- Click Start Test to run the collection.
3. View Results:
- Once the tests are complete, view the results in the Runner tab.
- Detailed test results can be viewed for each request.
## Testing
## Test Case Scenarios:
## _1. Create New Booking_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method:
## POST

### Pre-request Script:
```bash
var Vfirstname = pm.variables.replaceIn("{{$randomFirstName}}")   ///first name
console.log(Vfirstname)
pm.environment.set("firstname", Vfirstname)

var Vlastname = pm.variables.replaceIn("{{$randomLastName}}")     ///last name
console.log(Vlastname)
pm.environment.set("lastname", Vlastname)

var TotPrice = pm.variables.replaceIn("{{$randomInt}}")  ///Total price
pm.environment.set("TotPrice", TotPrice)

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")   ///Deposi tPaid
pm.environment.set("depositPaid", depositPaid)


var additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}")  /// Additional Needs
pm.environment.set("additionalNeeds", additionalNeeds)

const moment = require('moment')
const today = moment()
pm.environment.set("checkin", today.add(1, 'day').format("YYYY-MM-DD"))  ///checkin
pm.environment.set("checkout", today.add(5, 'day').format("YYYY-MM-DD")) ///checkout

```

### Request Body:
```bash
 {
	"firstname" : "{{firstname}}",
	"lastname" : "{{lastname}}",
	"totalprice" : {{TotPrice}},
	"depositpaid" : {{depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "{{additionalNeeds}}"
}

```

### Renponse Body:
```bash
  {
    "bookingid": 225,
    "booking": {
        "firstname": "Imogene",
        "lastname": "Hegmann",
        "totalprice": 163,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2024-05-01",
            "checkout": "2024-05-06"
        },
        "additionalneeds": "microchip"
    }
}
```

## _2. Get Booking Details By ID_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid

## Request Method: 
# GET
## Response Body:
```bash
{
    "firstname": "Imogene",
    "lastname": "Hegmann",
    "totalprice": 163,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-05-01",
        "checkout": "2024-05-06"
    },
    "additionalneeds": "microchip"
}
```

## _3. Create A Token For Authentication._
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: 
## POST
### Pre-request Script: None
### Request Body:

```bash
  {
    "username": "admin",
    "password": "password123"
 }
```

### Renponse Body:

```bash
  {
   "token": "06eb798bf6f2caa"
}
```
## _4. Update the Booking Details_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid

### Request Method: 
## PUT
### Pre-request Script:

```bash
var Vfirstname = pm.variables.replaceIn("{{$randomFirstName}}")   ///first name
console.log(Vfirstname)
pm.environment.set("firstname", Vfirstname)

var Vlastname = pm.variables.replaceIn("{{$randomLastName}}")     ///last name
console.log(Vlastname)
pm.environment.set("lastname", Vlastname)

var TotPrice = pm.variables.replaceIn("{{$randomInt}}")  ///Total price
pm.environment.set("TotPrice", TotPrice)

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")   ///Deposi tPaid
pm.environment.set("depositPaid", depositPaid)


var additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}")  /// Additional Needs
pm.environment.set("additionalNeeds", additionalNeeds)

const moment = require('moment')
const today = moment()
pm.environment.set("checkin", today.add(1, 'day').format("YYYY-MM-DD"))  ///checkin
pm.environment.set("checkout", today.add(5, 'day').format("YYYY-MM-DD")) ///checkout

```
### Request Body:
```bash
   {
	"firstname" : "{{firstname}}",
	"lastname" : "{{lastname}}",
	"totalprice" : {{TotPrice}},
	"depositpaid" : {{depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{checkin}}",
    	"checkout" : "{{checkout}}"
	},
	"additionalneeds" : "{{additionalNeeds}}"
}

```
### Renponse Body:
```bash
    {
     "bookingid": 4334,
     "booking": {
         "firstname": "Joelle",
         "lastname": "Krajcik",
         "totalprice": 266,
         "depositpaid": true,
         "bookingdates": {
             "checkin": "2024-03-15",
             "checkout": "2024-03-20"
         },
         "additionalneeds": "monitor"
     }
 }
```
## _5. Delete Booking Record_ 
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method:
## DELETE
### Response Body: None
## Run Command:
- Run Command for Console:

```bash
   newman run Booking_Site_API_Testing.postman_collection.json -e booking-api.postman_environment.json
```
- Run Command for Report:
```bash
   newman run Booking_Site_API_Testing.postman_collection.json -e booking-api.postman_environment.json -r cli,htmlextra
```
## Newman Report Summary:
![image](https://github.com/mmahabubalam/Booking-Site-API-Testing/assets/149142080/99a887fb-1189-4a09-96e9-39f8ec1dd6d3)
![image](https://github.com/mmahabubalam/Booking-Site-API-Testing/assets/149142080/21b8d766-8107-46af-9edc-1b19feb0307b)
![image](https://github.com/mmahabubalam/Booking-Site-API-Testing/assets/149142080/cc155e61-9724-4384-b076-f4673a2cfe91)
![image](https://github.com/mmahabubalam/Booking-Site-API-Testing/assets/149142080/119991f1-0a8a-4506-8ab4-c16422fe5bab)

