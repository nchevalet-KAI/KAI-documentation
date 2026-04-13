---
description: >-
  The Orchestrator endpoints drive document indexation: starting jobs, tracking
  their status, and managing re-indexation.
---

# Orchestrator

_Authenticated with `instance-id` + `api-key` headers — see Instance API keys._

***

{% openapi-operation spec="KAI-Instance-API" path="/api/orchestrator/check-kb-credentials" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/orchestrator/count-back-tasks" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/orchestrator/count-tasks-for-doc" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/orchestrator/differential-indexation" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/orchestrator/reindex-document" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="KAI-Instance-API" path="/api/orchestrator/retry-documents-parsing-error" method="post" %}
[OpenAPI KAI-Instance-API](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/89f6938646269cfb1668efd1e6d895e64c59a976ebdcab757910ecee14fc92c0.yaml?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260413%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260413T094034Z&X-Amz-Expires=172800&X-Amz-Signature=8f7a9d93ee9d3527f481fbaa1bb0c9677abe05e9df01e7d56661ade859505551&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
