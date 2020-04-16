---
page_type: sample
description: "How to build an MVC web application that performs identity management with Azure AD B2C using the ASP.Net Core OpenID Connect middleware."
languages:
  - csharp
products:
  - dotnet-core
  - aspnet-core
  - azure
  - azure-active-directory
---

# An ASP.NET Core web app with Azure AD B2C 
This sample shows how to build an MVC web application that performs identity management with Azure AD B2C using the ASP.Net Core OpenID Connect middleware.  It assumes you have some familiarity with Azure AD B2C.  If you'd like to learn all that B2C has to offer, start with our documentation at [aka.ms/aadb2c](http://aka.ms/aadb2c). 

The app is a basic web application that performs three functions: sign-in, sign-up, and sign-out.  It is intended to help get you started with Azure AD B2C in a ASP.NET Core application, giving you the necessary tools to execute Azure AD B2C policies & securely identify uses in your application.  

## How To Run This Sample

To run this sample you will need:

- To install .NET Core for Windows by following the instructions at [dot.net/core](http://dot.net/core), which will include Visual Studio 2017.
- An Internet connection
- An Azure subscription (a free trial is sufficient)

### Step 1:  Clone or download this repository

From your shell or command line:

```powershell
git clone https://github.com/JimXu199545/NetCoreWeb.git
```

### [OPTIONAL] Step 2: Get your own Azure AD B2C tenant

You can also modify the sample to use your own Azure AD B2C tenant.  First, you'll need to create an Azure AD B2C tenant by following [these instructions](https://azure.microsoft.com/documentation/articles/active-directory-b2c-get-started).

> *IMPORTANT*: if you choose to perform one of the optional steps, you have to perform ALL of them for the sample to work as expected.

### [OPTIONAL] Step 3: Create your own policies

This sample uses three types of policies: a unified sign-up/sign-in policy, a profile editing policy and a password reset policy.  Create one policy of each type by following [the instructions here](https://azure.microsoft.com/documentation/articles/active-directory-b2c-reference-policies).  You may choose to include as many or as few identity providers as you wish.

If you already have existing policies in your Azure AD B2C tenant, feel free to re-use those.  No need to create new ones just for this sample.

### [OPTIONAL] Step 4: Create your own Web API

This sample calls an API at https://fabrikamb2chello.azurewebsites.net which has the same code as the sample [Node.js Web API with Azure AD B2C](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi). You'll need your own API or at the very least, you'll need to [register a Web API with Azure AD B2C](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-api) so that you can define the scopes that your single page application will request access tokens for. 

Your web API registration should include the following information:

- Enable the **Web App/Web API** setting for your application.
- Set the **Reply URL** to the appropriate value indicated in the sample or provide any URL if you're only doing the web api registration, for example `https://myapi`.
- Make sure you also provide a **AppID URI**, for example `demoapi`, this is used to construct the scopes that are configured in you single page application's code.
- (Optional) Once you're app is created, open the app's **Published Scopes** blade and add any extra scopes you want.
- Copy the **AppID URI** and **Published Scopes values**, so you can input them in your application's code.

### [OPTIONAL] Step 5: Create your own Web app

Now you need to [register your web app in your B2C tenant](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-application), so that it has its own Application ID. Don't forget to grant your application API Access to the web API you registered in the previous step.

Your native application registration should include the following information:

- Enable the **Web App/Web API** setting for your application.
- Set the **Reply URL** to `https://localhost:5000/signin-oidc`.
- Once your app is created, open the app's **Keys** blade and click on **Generate Key** and **Save**, copy this key so that you can used it in the next step.
- Once your app is created, open the app's **API access** blade and **Add** the API you created in the previous step.
- Copy the Application ID generated for your application, so you can use it in the next step.

### [OPTIONAL] Step 6: Configure the sample with your app coordinates

1. Open the solution in Visual Studio.
1. Open the `appsettings.json` file.
1. Find the assignment for `Tenant` and replace the value with your tenant name.
1. Find the assignment for `ClientID` and replace the value with the Application ID from Step 5.
1. Find the assignment for each of the policies `XPolicyId` and replace the names of the policies you created in Step 3.
1. Find the assignment for `ClientSecret` and replace the value with App Key you created in Step 5.
1. Find the assignment for `ApiUrl` and replace the value with the URL of the API that you registered in Step 4.
1. Find the assignment for the `ApiScopes` and replace the scopes with those you created in Step 4.

```json
{
  "Authentication": {
    "AzureAdB2C": {
      "ClientId": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6",
      "Tenant": "fabrikamb2c.onmicrosoft.com",
      "SignUpSignInPolicyId": "b2c_1_susi",
      "ResetPasswordPolicyId": "b2c_1_reset",
      "EditProfilePolicyId": "b2c_1_edit_profile",
      "RedirectUri": "http://localhost:5000/signin-oidc",
      "ClientSecret" : "v0WzLXB(uITV5*Aq",
      "ApiUrl": "https://fabrikamb2chello.azurewebsites.net/hello",
      "ApiScopes": "https://fabrikamb2c.onmicrosoft.com/demoapi/demo.read"
    }
  }
}
```

### Step 7:  Run the sample

Clean the solution, rebuild the solution, and run it.  You can now sign up & sign in to your application using the accounts you configured in your respective policies.

