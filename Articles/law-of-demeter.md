## **Law of Demeter**

Talk to friends, not to strangers. In OOP what it means, is that to get its work done a class can make use of methods and properties of its dependencies, and not of dependencies of dependencies.       

Violation of this law makes the code difficult to test. 

An example of a violation of this law may look like this: 

`string userName = sessionService.GetSession().GetLogin().GetUser().GetUserName();`

The class with this piece of code, prima facie may seem to be dependent upon only session service, but in reality, because of this line code, it has additionally become dependent upon session object, login object, and user object.  So now, to test this functionality, not only the session service needs to be mocked, but three additional dependencies would also need to be mocked. 

We can resolve this issue, by injecting an Identity service that directly exposes GetUserName method. 

`string userName = identityService.GetUserName();` 

Now the class would only be making use of a method of its direct dependency, and so abides by the Law of Demeter. Testing this class would be much easier because now only  `IdentityService` would need to be mocked.