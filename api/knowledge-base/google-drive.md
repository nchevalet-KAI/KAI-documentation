---
description: Connect Google Drive to KAI
---

# Google Drive

Need : Google Platform admin

To connect with Google Drive, we will use a Google Service Account to be able to use Google Drive API

Information about Google Service Account : [https://cloud.google.com/iam/docs/service-account-overview](https://cloud.google.com/iam/docs/service-account-overview)

Information about Google Drive API : [https://developers.google.com/workspace/drive/api/guides/about-sdk](https://developers.google.com/workspace/drive/api/guides/about-sdk)

{% stepper %}
{% step %}
### Generate a service account json file

Here the documentation to create a service account : [https://cloud.google.com/iam/docs/service-accounts-create](https://cloud.google.com/iam/docs/service-accounts-create)

Your service account will have an email as identifier
{% endstep %}

{% step %}
### Attach the Google Drive API to the service account

On the service account created, on the menu "API", add Google Drive API into the created service account.
{% endstep %}

{% step %}
### Download the google service account json file

On the service account page, go to "keys" tab.

Click on "Add a key" and select JSON.

You will have the possibility to download the json file now.
{% endstep %}

{% step %}
### Attach the service account to a google drive folder

On Google Drive, add your service account (reader only) on the google drive folder you want to index. You can find easily your service account by his email identifier (step 1).
{% endstep %}

{% step %}
### (OPTIONAL) To index only a subfolder of your Google Drive

In the case you only want to index a subfolder of your google drive (let's imagine you use this service account for multiple applications and for KAI you only want to index a sub folder). Note down the name of the folder.
{% endstep %}
{% endstepper %}

Final output :

* service\_acount: upload the service account json file downloaded on step 3
* folder\_name: if you want to only index a specified folder, fill it with the folder name retrieved on step 5, else let it blank
