---
hidden: true
icon: network-wired
---

# OpenAPI

You can sync GitBook pages with an OpenAPI or Swagger file or a URL to include auto-generated API methods in your documentation.

### OpenAPI block

GitBook's OpenAPI block is powered by [Scalar](https://scalar.com/), so you can test your APIs directly from your docs.

{% openapi-operation spec="k-ai-api-documents" path="/list-docs" method="post" %}
[OpenAPI k-ai-api-documents](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/9dba614e561d0358f094ef2f29d2b367638f55b7556dd2ca9efe6e8c3804008f.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250702%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250702T142859Z&X-Amz-Expires=172800&X-Amz-Signature=6e1c01d1299c93b9bc25344e49905aaf637f84c72d49680f98610214d961a6e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="k-ai-api-documents" path="/count-documents-by-state" method="post" %}
[OpenAPI k-ai-api-documents](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/9dba614e561d0358f094ef2f29d2b367638f55b7556dd2ca9efe6e8c3804008f.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250702%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250702T142859Z&X-Amz-Expires=172800&X-Amz-Signature=6e1c01d1299c93b9bc25344e49905aaf637f84c72d49680f98610214d961a6e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-operation spec="k-ai-api-documents" path="/doc" method="post" %}
[OpenAPI k-ai-api-documents](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/9dba614e561d0358f094ef2f29d2b367638f55b7556dd2ca9efe6e8c3804008f.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250702%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250702T142859Z&X-Amz-Expires=172800&X-Amz-Signature=6e1c01d1299c93b9bc25344e49905aaf637f84c72d49680f98610214d961a6e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

{% openapi-schemas spec="k-ai-api-documents" schemas="CountDocumentsByStateInput,DocumentExtraproperties,DocumentOutput,GetDocInput,GetDocOutput,HTTPValidationError,IntegerOutput,KbSignature,LightDocumentOutput,ListDocsInput,ListDocsOutput,ValidationError" grouped="true" %}
[OpenAPI k-ai-api-documents](https://gitbook-x-prod-openapi.4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/raw/9dba614e561d0358f094ef2f29d2b367638f55b7556dd2ca9efe6e8c3804008f.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20250702%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20250702T142859Z&X-Amz-Expires=172800&X-Amz-Signature=6e1c01d1299c93b9bc25344e49905aaf637f84c72d49680f98610214d961a6e8&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-schemas %}
