---
description: Connect your Confluence space with KAI
---

# Atlassian Confluence

need: Your Atlassian Confluence admin

{% stepper %}
{% step %}
### Create an Atlassian Service account

You will need to create a service account : [https://support.atlassian.com/user-management/docs/understand-service-accounts/](https://support.atlassian.com/user-management/docs/understand-service-accounts/)
{% endstep %}

{% step %}
### Create an api token attached to this service account

Here the documentation : [https://support.atlassian.com/user-management/docs/manage-api-tokens-for-service-accounts/](https://support.atlassian.com/user-management/docs/manage-api-tokens-for-service-accounts/)

Here scopes needed :&#x20;

* read:confluence-content.all
* search:confluence
* readonly:content.attachment:confluence
{% endstep %}

{% step %}
### Retrieve the server url of your confluence

If the url of your confluence is : https://k-ai-test.atlassian.net/wiki/spaces/EKT/pages/xxx

The server\_url to get back is : https://k-ai-test.atlassian.net
{% endstep %}

{% step %}
### Retrieve the name of the space

If the url of your confluence is : https://k-ai-test.atlassian.net/wiki/spaces/EKT/pages/xxx

The space to get back is : EKT
{% endstep %}
{% endstepper %}

Final output :&#x20;

* serverUrl : is the server\_url you get back on step 3
* userName : is the user name of your atlassian service account created on step 1
* password : is the api token generated on step 2
* space : is the space retrieved on step 4

