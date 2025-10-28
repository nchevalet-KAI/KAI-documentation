---
description: Index documents uploaded on your Snowflake stage
---

# Snowflake stage

Need : Snowflake admin

### General case (use a Snowflake Stage on the KAI SaaS Version)

{% stepper %}
{% step %}
### Create a snowflake user

[https://docs.snowflake.com/en/sql-reference/sql/create-user](https://docs.snowflake.com/en/sql-reference/sql/create-user)
{% endstep %}

{% step %}
### Create an programatic access token for this user

[https://docs.snowflake.com/en/user-guide/programmatic-access-tokens](https://docs.snowflake.com/en/user-guide/programmatic-access-tokens)
{% endstep %}

{% step %}
### Create a role to access to the snowflake stage

[https://docs.snowflake.com/en/sql-reference/sql/create-stage#access-control-requirements](https://docs.snowflake.com/en/sql-reference/sql/create-stage#access-control-requirements)
{% endstep %}

{% step %}
### Attach the role to the user

[https://docs.snowflake.com/en/sql-reference/sql/grant-role](https://docs.snowflake.com/en/sql-reference/sql/grant-role)
{% endstep %}

{% step %}
### Retrieve your snowflake account information

On the snowflake web application, bottom left, click on your account and click on your account detail.

Information to note down :&#x20;

* account identifier
{% endstep %}
{% endstepper %}

Final output :&#x20;

* account : The account identifier of your snowflake tenant retrieved on step 5
* database : The database name where is holded the stage
* schema : the schema name where is holded the stage
* role : the role who has access to the stage and granted to the user on step 3
* user : the username of the created snowflake user on step 1
* password : the programatic access token created on step 2
* stage name : the name of the stage you want to connect
* type : EXTERNAL

### In case you want to connect a Snowflake Stage with KAI app through Snowflake&#x20;

In this case, we will use the snowflake rules management and give access to the Snowflake stage you want to connect with the KAI app through Snowflake rules.

Need : Snowflake Admin

{% stepper %}
{% step %}
### Configure the stage for the KAI app

When you deploy KAI app, a app name is asked to configure (and only visible on your side), note it down.

consumer\_db = the database where your stage is

consumer\_schema = the schema where your stage is

consumer\_stage = your snowflake stage name

app\_name = the name you choose when you deploy KAI on your snowflake account.

```sql
GRANT USAGE ON DATABASE <consumer_db> TO APPLICATION <app_name>; 
GRANT USAGE ON SCHEMA <consumer_db>.<consumer_schema> TO APPLICATION <app_name>; 
GRANT READ ON STAGE <consumer_db>.<consumer_schema>.<consumer_stage> TO APPLICATION <app_name>;
```

These commands will give the possibility to the KAI app to read documents of your Snowflake Stage.
{% endstep %}
{% endstepper %}

Final output :&#x20;

* account : put "account" (will not be used, the value is not a matther)
* database : consumer\_db
* schema : consumer\_schema
* role : put "role" (will not be used, the value is not a matter)
* user : put "user" (will not be used, the value is not a matter)
* password : put "password" (will not be used, the value is not a matter)
* stage name : consumer\_stage
* type : INTERNAL

