---
description: Index documents uploaded on your Snowflake stage
---

# Snowflake stage

Need : Snowflake admin

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
