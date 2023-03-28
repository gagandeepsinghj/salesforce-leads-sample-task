# Problem Statement

You are working as a Salesforce developer *at Brand Outreach Inc*. Brand Outreach have APIs exposed for various purposes. Your task is to:

 - Generate an RSA private/public keypair. Feel free to use an online tool to generate the key pair.
 - Store the private key in your Salesforce instance. Note: A private key is a confidential piece of information, so, make sure that it's stored securely and follows Salesforce's security best practices.
 - Write a job that:
	 - Runs daily (midnight)
	 - Generates an auth token by signing the payload with a private key. You can use [Crypto class methods](https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_classes_restful_crypto.html) to do this.
	 - Calls the `/users` [API](https://dummyjson.com/users) to fetch the users from marketing department.
	 - Creates corresponding `Contact` records in Salesforce.
	 - Write test cases to test your implementation

## Payload
You will need the following data to sign it with a private key
 ```
{ 
	"iss": "sfdc_service", 
	"aud": "https://login.salesforce.com", 
	"sub": << email address of the logged in Salesforce admin >>, 
	"iat": << current time >>, 
	"exp": << current time + 3 minutes >>, 
	"jti": << random uuid >> 
}
```

**Example Input**
```
{ 
	"iss": "sfdc_gateway", 
	"aud": "https://salesforce.com", 
	"sub": "gagan.singh@influitive.com", 
	"iat": 1679974871, 
	"exp": 1679975059, 
	"jti": "f90cde94-5b43-4940-ad03-beb549c233b2" 
}
```
**Example Output**
```
AVHx1IWzEFJ94ZqGJmUlLa_6lotbBPDpCeBlQS9_AtSCnjtGKKyMKxbkRV6lA2hRQBGzO8FaFryPP-vZQfJcBbZvABsrS-DZH556fp6mCKvP-rUyB2jXVi9sYaQL2tJfPWmknK-wY_UB9FZHLTsO800mwIEVGzJgicOWdiouBec-4CLt
```

## Calling the API
**URL:** 
```https://dummyjson.com/users```

**Headers:**
```
 - Content-Type: application/json
 - Authorization: Bearer << signed token >>
```
**Parameters**
```
key=department
value=marketing
```

**Sample Response**
```
{
	"users": {
		[{
			"id": 1,
			"firstName": "Terry",
			"lastName": "Medhurst",
			"maidenName": "Smitham",
			"age": 50,
			"gender": "male",
			"email": "atuny0@sohu.com",
			"phone": "+63 791 675 8914",
			"username": "atuny0"
		}]
	}
}
```