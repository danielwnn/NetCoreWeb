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



### [OPTIONAL] Step 4: Create your own Web app

Now you need to [register your web app in your B2C tenant](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-app-registration#register-a-web-application), so that it has its own Application ID. Don't forget to grant your application API Access to the web API you registered in the previous step.

Your native application registration should include the following information:

- Enable the **Web App/Web API** setting for your application.
- Set the **Reply URL** to `https://localhost:44381/signin-oidc`.
- Once your app is created, open the app's **Keys** blade and click on **Generate Key** and **Save**, copy this key so that you can used it in the next step.
- Once your app is created, open the app's **API access** blade and **Add** the API you created in the previous step.
- Copy the Application ID generated for your application, so you can use it in the next step.

### [OPTIONAL] Step 5: Configure the sample with your app coordinates

1. Open the solution in Visual Studio.
1. Open the `appsettings.json` file.
1. Find the assignment for `Tenant` and replace the value with your tenant name.
1. Find the assignment for `ClientID` and replace the value with the Application ID from Step 4.
1. Find the assignment for each of the policies `XPolicyId` and replace the names of the policies you created in Step 3.
1. Find the assignment for `ClientSecret` and replace the value with App Key you created in Step 4.


```json
{
  "Authentication": {
    "AzureAdB2C": {
      "ClientId": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6",
      "Tenant": "fabrikamb2c.onmicrosoft.com",
      "SignUpSignInPolicyId": "b2c_1_susi",
      "ResetPasswordPolicyId": "b2c_1_reset",
      "EditProfilePolicyId": "b2c_1_edit_profile",
      "RedirectUri": "https://localhost:44381/signin-oidc",
      "ClientSecret" : "v0WzLXB(uITV5*Aq"
    }
  }
}
```

### Step 6:  Run the sample

Clean the solution, rebuild the solution, and run it.  You can now sign up & sign in to your application using the accounts you configured in your respective policies.

