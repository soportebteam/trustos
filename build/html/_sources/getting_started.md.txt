# Getting Started

Why worrying about the low-level complexities of blockchain technology,
and having to worry about building you network when you can leverage
the benefits of the technology without having to know the details of
its operation. Our TrustOS abstracts all the complexity of blockchain
technology implementing the basic operations you need to leverage
the power of blockchain technology. 

## Login


In order to use the APIs, you need to have an active user and login to our system. Every API has a login method, which asks for a user and password.

A call to this method will return a JWT token, of this form:

```
{
  "message": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdCIsImV4cCI6MTU2MDAwMDE5MH0.M4PBSslERUImcOpWgg--N-2ZNW306BzWXTZVJgtdXWE"
}

```

Every call to the API, has to be authenticated, so the caller must provide this message as proof of his identity.

Add the following header to your HTTP request in order to authenticate your call: 

```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdCIsImV4cCI6MTU2MDAwMDE5MH0.M4PBSslERUImcOpWgg--N-2ZNW306BzWXTZVJgtdXWE
```


If you are calling the APIs from Postman, you can set manually the headers (there are examples in the miscelanea/postman folder)

However if you interact graphically with the swagger,  you have to click the button **authorize, on the top right** of the screen.


From there, in the "value" field of ApiKeyAuth, you should write:
```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoidGVzdCIsImV4cCI6MTU2MDAwMDE5MH0.M4PBSslERUImcOpWgg--N-2ZNW306BzWXTZVJgtdXWE
```

You should now see that all the locks in swagger are closed, meaning that you are authenticated! 

The test user for this beta version is :
```
username : example
password : example
```

