# Audit (raw primitives)

{% hint style="warning" %}
**Do not confuse with the Audit API.** These endpoints are raw audit primitives exposed by the instance itself — low-level counters and flags, consumed machine-to-machine. The full audit workflow (state machine, duplicates, conflicts, questions, MCP integration) lives on the separate **Audit API** at `api-audit.kai-studio.ai`.
{% endhint %}

_Authenticated with `instance-id` + `api-key` headers — see Instance API keys._

***

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/conflict-information" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/conflict-information/set-state" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/count-conflict-by-date" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/count-conflict-by-document-ids" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/count-conflict-by-subject" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/count-conflict-information" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/count-conflicts-by-state" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/document-ids-to-manage" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/document-is-analyzed" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/get-anomalies-for-document" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/get-conflict-document-pair" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/get-conflict-information" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/get-conflict-information-by-subject" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/get-conflicts-by-document-id-pair" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/audit/list-all-document-ids" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
