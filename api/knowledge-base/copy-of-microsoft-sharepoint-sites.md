---
description: To connect KAI with Microsoft Sharepoint, we use Microsoft Graph API
---

# Copy of Microsoft Sharepoint (sites)

Need : your Microsoft Azure Tenant Administrator

{% stepper %}
{% step %}
### Create an Azure App Registration

[https://learn.microsoft.com/en-us/graph/auth-register-app-v2](https://learn.microsoft.com/en-us/graph/auth-register-app-v2)
{% endstep %}

{% step %}
### Create a secret key on your azure app registration

[https://learn.microsoft.com/en-us/graph/auth-register-app-v2#option-2-add-a-client-secret](https://learn.microsoft.com/en-us/graph/auth-register-app-v2#option-2-add-a-client-secret)
{% endstep %}

{% step %}
### Add scopes

[https://learn.microsoft.com/en-us/graph/permissions-overview?tabs=http](https://learn.microsoft.com/en-us/graph/permissions-overview?tabs=http)

here scopes needed :&#x20;

* Files.Read.All \[application permission]
* Group.Read.All \[application permission]
* Sites.Read.All \[application permission]
{% endstep %}

{% step %}
### (OPTIONAL) Select only sharepoint you want to connect on KAI

[https://learn.microsoft.com/fr-fr/sharepoint/dev/sp-add-ins-modernize/understanding-rsc-for-msgraph-and-sharepoint-online](https://learn.microsoft.com/fr-fr/sharepoint/dev/sp-add-ins-modernize/understanding-rsc-for-msgraph-and-sharepoint-online)
{% endstep %}

{% step %}
### Retrieve your sharepoint host

example : if your sharepoint url look like this : https://contoso.sharepoint.com/sites/Tech

Your sharepoint host is : contoso.sharepoint.com
{% endstep %}

{% step %}
### Retrieve your sharepoint site name

Example : if your sharepoint url look like this : https://contoso.sharepoint.com/sites/Tech

Your sharepoint site name is : Tech


{% endstep %}
{% endstepper %}

Final output :&#x20;

* tenant id : the tenant id of your Microsoft Azure tenant where is linked to your Microsoft Sharepoint
* client id : application client id of the app registration&#x20;
* client secret : secret key generated during the phase 2 of your app registration
* sharepoint host : the sharepoint host of your Microsoft Sharepoint
* sharepoint site name : the sharepoint site retrieved on phase 6

