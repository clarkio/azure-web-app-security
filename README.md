# azure-web-app-security
A place to record and save details on my learnings in securing web based applications (in general JavaScript) in Azure

## Authentication

### Azure Functions
This uses App Service behind the scenes and configuring for Azure Functions is a similar process to App Service.

**Notes:**
> Authentication/Authorization not supported for Linux yet. Must choose Windows when create a new Azure Functions App

> Had to follow this post to figure out how to easily connect the authentication with Twitter to a web app and the Azure Function: [link](https://blogs.msdn.microsoft.com/stuartleeks/2018/02/19/azure-functions-and-app-service-authentication/)

> Maybe need this SDK in the client? [link](https://github.com/Azure/azure-mobile-apps-js-client)

**** Another limitation** is that you are currently required (though there’s a workaround) to use token based authentication and not cookie based authentication: [GitHub issue](https://github.com/Azure/azure-functions-host/issues/620)

This documentation was helpful to figure out possible query parameters on login request: [link](https://github.com/cgillum/easyauth/wiki/Login#server-directed-login)

#### Steps to add authentication/authorization
1. Create a windows based azure function app
2. Under “Platform Features” click “Authentication/Authorization”
3. Under “App Service Authentication” select “On” 
4. Under “Action to take when request is not authenticated” choose the login service provider you’d like to use
    
    Example: “Log in with Twitter”

5. Under “Authentication Providers” be sure to configure the login provider you chose
    
    Example: For Twitter we enter an API Key and Secret

6. Under “Allowed External Redirect URLs” add the callback URLs you plan to use.
    
    Example: http://localhost:3000/
    > Note: at the time of this writing (9/5/2018) you cannot add “localhost” in the domain and instead need to use “127.0.0.1”

7. Update CORS for your client application domain
