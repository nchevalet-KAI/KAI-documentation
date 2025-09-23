---
description: Connect your Service Now Knowledge Base with KAI
---

# Service Now

need : Your Service Now admin

We will use the [knowledge base api rest](https://www.servicenow.com/docs/bundle/zurich-api-reference/page/integrate/inbound-rest/concept/knowledge-api.html) method to connect to your knowledge base&#x20;

{% stepper %}
{% step %}
### Activate the Knowledge API module (free)

Here the link to activate the module : [https://store.servicenow.com/store/app/2d6d23261b646a50a85b16db234bcb49#linksAndDocuments](https://store.servicenow.com/store/app/2d6d23261b646a50a85b16db234bcb49#linksAndDocuments)
{% endstep %}

{% step %}
### Create a service account

Create a service account on Service Now admin panel : [https://www.servicenow.com/community/in-other-news/user-account-or-service-account-what-to-use-for-web-service/ba-p/2286977](https://www.servicenow.com/community/in-other-news/user-account-or-service-account-what-to-use-for-web-service/ba-p/2286977)
{% endstep %}

{% step %}
### Retrieve the KB ID of the knowledge base you want to index into KAI

In the nav bar (left menu), open the **knowledge bases**, you will see all knowledge base you have created.

Click on the knowledge base you want to connect.

The url of the opened page will be formated like that : https://kai-test.service-now.com/kb\_knowledge\_base.do?sys\_id=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

Your KB ID will be : xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
{% endstep %}

{% step %}
### Retrieve your service now domain

If your url look like that : https://kai-test.service-now.com/xxx

Your domain will be : kai-test.service-now.com
{% endstep %}
{% endstepper %}

Final output :&#x20;

* domain : the domain retrieved on step 4
* user : the user of the service account generated on step 2
* password : the password of the service account generated on step 2
* kb\_id: the id of the knowledge base you want to index on KAI retrieved on step 3
