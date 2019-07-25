# Best Practices
A guide for programming well.
Extracted from Thoughbot.

## General
- These are not to be blindly followed; strive to understand these and ask when in doubt.
- Don't duplicate the functionality of a built-in library.
- Don't swallow exceptions or "fail silently."
- Don't write code that guesses at future functionality.
- Exceptions should be exceptional.
- Keep the code simple.

## REST APIs
Extracted from the work on some blogs.

### Terminologies
- **Resource** is an object or representation of something, which has some associated data with it and there can be set of methods to operate on it.
E.g. Animals, schools and employees are resources and delete, add, update are the operations to be performed on these resources.
- **Collections** are set of resources, e.g Companies is the collection of Company resource.
- **URL (Uniform Resource Locator)** is a path through which a resource can be located and some actions can be performed on it.

### Conventions
The URL should only contain resources(nouns) not actions or verbs.

This is where the HTTP methods (GET, POST, DELETE, PUT), also called as verbs, play the role.

### HTTP Methods
#### GET
Method requests data from the resource and should not produce any side effect.

E.g /companies/2/employees returns list of all employees from company 2.

/companies should get the list of all companies

/companies/7 should get the detail of company 7

/companies/2/employees should get the list of all employees from company 2

/companies/2/employees/87 should get the details of employee 87, which belongs to company 2

#### POST
Method requests the server to create a resource in the database, mostly when a web form is submitted.

E.g /companies/2/employees creates a new Employee of company 2.

/companies should create a new company and return the details of the new company created
> POST is non-idempotent which means multiple requests will have different effects.

#### PUT
Method requests the server to update resource or create the resource, if it doesn’t exist.

E.g. /companies/2/employees/mike will request the server to update, or create if doesn’t exist, the *mike* resource inemployeescollection under company 2.
> PUT is idempotent which means multiple requests will have the same effects.

#### DELETE:
Method requests that the resources, or its instance, should be removed from the database.

E.g /companies/2/employees/mike/ will request the server to delete mike resource from the employees collection under the company 2.

/companies/7 should delete company 7

/companies/2/employees/87 should delete employee 87, which belongs to company 2

### Responses
- 2xx (Success category)
- 3xx (Redirection Category)
- 4xx (Client Error Category)
- 5xx (Server Error Category)

### Other
#### Sorting
In case, the client wants to get the sorted list of companies, the GET /companies endpoint should accept multiple sort params in the query.

E.g GET /companies?sort=rank_asc would sort the companies by its rank in ascending order.

#### Filtering
For filtering the dataset, we can pass various options through query params.

E.g GET /companies?category=banking&location=india would filter the companies list data with the company category of Banking and where the location is India.

#### Searching
When searching the company name in companies list the API endpoint should be GET /companies?search=Digital Mckinsey

#### Pagination
When the dataset is too large, we divide the data set into smaller chunks, which helps in improving the performance and is easier to handle the response.

Eg. GET /companies?page=23 means get the list of companies on 23rd page.

### Versioning
Upgrading the APIs with some breaking change would also lead to breaking the existing products or services using your APIs.

http://api.yourservice.com/v1/companies/7/employees is a good example, which has the version number of the API in the path. If there is any major breaking update, we can name the new set of APIs as v2 or v1.x.x

### Field name casing convention
If the request body or response type is JSON then please follow snake_case to maintain the consistency.
