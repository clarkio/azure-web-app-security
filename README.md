# azure-web-app-security
A place to record and save details on my learnings in securing web based applications (in general JavaScript) in Azure

## TODO
- [ ] figure out how to run and test authentication locally with azure functions
- [ ] figure out how to run and test authentication locally with node.js api (to be hosted in app service)

## Authentication

### Azure Functions
This uses App Service behind the scenes and configuring for Azure Functions is a similar process to App Service.

**Notes:**
> Authentication/Authorization not supported for Linux yet. Must choose Windows when create a new Azure Functions App

> Had to follow this post to figure out how to easily connect the authentication with Twitter to a web app and the Azure Function: [link](https://blogs.msdn.microsoft.com/stuartleeks/2018/02/19/azure-functions-and-app-service-authentication/?WT.mc_id=academic-0000-brcl)

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
    
    Example: http://127.0.0.1:3000/ and see note below
    > Note: Use 127.0.0.1 instead of localhost. At the time of this writing (9/5/2018) you cannot add “localhost” due to input validation in the portal

7. Update CORS for your client application domain

    Example: http://127.0.0.1:3000/
    
8. 
    
   
#### Corresponding Azure Docs
- [Login with Twitter](https://docs.microsoft.com/azure/app-service/app-service-mobile-how-to-configure-twitter-authentication?WT.mc_id=academic-0000-brcl)
- [Login with Microsoft Account](https://docs.microsoft.com/azure/app-service/app-service-mobile-how-to-configure-microsoft-authentication?WT.mc_id=academic-0000-brcl)
- [Login Customization and Logout Details](https://docs.microsoft.com/azure/app-service/app-service-authentication-how-to?WT.mc_id=academic-0000-brcl)
