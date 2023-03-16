### Problem Statement:

##### You are working on a customer referral management system that tracks customer referrals for new leads. You are given two custom Salesforce objects: `Customer__c` and `Lead__c`. The `Customer__c` object has the following fields:

-   `Id`: A unique identifier for the customer
-   `Name`: The name of the customer
-   `Email__c`: The email address of the customer

##### The `Lead__c` object has the following fields:

-   `Id`: A unique identifier for the lead
-   `Name__c`: The name of the lead
-   `Email__c`: The email address of the lead
-   `Status__c`: A picklist field with values 'Open', 'Closed', and 'Converted'

*Write a Salesforce Apex method that takes in a `Lead__c` object as input and returns a list of customers who have referred the lead. A referral is considered valid if the referred customer's email address matches the email address of the lead.*

### Input:

-   A `Lead__c` object

### Output:

-   A list of `Customer__c` objects who have made valid referrals for the given `Lead__c` object

### Example Input:

`Lead__c(Id='XYZ123', Name__c='John Smith', Email__c='john.smith@company.com', Status__c='Open')`

### Example Output:

`[
   Customer__c(Id='C001', Name='Jane Doe', Email__c='jane.doe@company.com'),
   Customer__c(Id='C002', Name='Bob Johnson', Email__c='bob.johnson@company.com')
 ]`
