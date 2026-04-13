# Instance API keys

The **KAI Instance API** (`https://api.kai-studio.ai`) uses static API-key authentication. Every request must carry two headers.

### Obtaining credentials

* Go to your KAI admin portal → **Instances** → select your instance → **API credentials**.
* Copy the `instance_id` and `api_key`.
* If you do not have access to the admin portal, contact KAI support.

### Request headers

```http
instance-id: <your-instance-id>
api-key: <your-api-key>
Content-Type: application/json
```

_(Exact header names are `instance-id` and `api-key`, lowercase with hyphens.)_

### Scope & isolation

One `(instance_id, api_key)` pair grants access to **exactly one instance**. Permissions are not user-level — there is no notion of "user" on this API. Any caller presenting the correct headers has full instance access.

### Rotation

To rotate a compromised key:

1. Admin portal → **Instances** → **Regenerate API key**.
2. The previous key is revoked immediately.
3. Update any deployed integrations with the new value.

{% hint style="warning" %}
**Never expose an instance API key in client-side code** (browsers, mobile apps, public widgets). This is a machine-to-machine credential only. For user-facing scenarios, use the **Retrieval API** with OAuth 2.1 instead.
{% endhint %}
