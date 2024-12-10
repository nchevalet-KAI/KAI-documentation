---
icon: webhook
description: >-
  An API testing interface is available on Postman :
  https://documenter.getpostman.com/view/30765019/2s9YXcek45
---

# API

Our API is organized into four types of endpoints :

Find all endpoints on Postman [here](https://documenter.getpostman.com/view/30765019/2s9YXcek45) .

<details>

<summary>Core : for basic and central functions</summary>

Endpoints about the documents KAI accesses, analayze, indexes :

[/api/orchestrator/differential-indexation](https://documenter.getpostman.com/view/30765019/2s9YXcek45#674dea09-1167-437b-a57a-c7a89186d438)\
[/api/orchestrator/files/download](https://documenter.getpostman.com/view/30765019/2s9YXcek45#46b0acc7-ed4b-4e01-81a3-99afe06157bd)\
[/api/orchestrator/list-docs](https://documenter.getpostman.com/view/30765019/2s9YXcek45#d8dfec95-b0fe-440d-b403-2bea25826841)\
[/api/orchestrator/stats/count-detected-documents](https://documenter.getpostman.com/view/30765019/2s9YXcek45#a5239f86-408f-4a75-8dff-c144769965e6)\
[/api/orchestrator/stats/count-documents](https://documenter.getpostman.com/view/30765019/2s9YXcek45#ee1a63bf-ada8-4008-835b-109b23e92e74)\
[/api/orchestrator/stats/count-indexable-documents\
](https://documenter.getpostman.com/view/30765019/2s9YXcek45#29c64934-89e8-4cb9-9cbd-c8df6ebbfe9d)[/api/orchestrator/stats/count-indexed-documents](https://documenter.getpostman.com/view/30765019/2s9YXcek45#a5239f86-408f-4a75-8dff-c144769965e6)

End points about the system :

[/global-health\
](https://documenter.getpostman.com/view/30765019/2s9YXcek45#847a6099-2c21-4101-bced-e345b43bd88e)[/health\
](https://documenter.getpostman.com/view/30765019/2s9YXcek45#257542f2-cb13-4a5a-b657-464f039c43e7)[/version](https://documenter.getpostman.com/view/30765019/2s9YXcek45#b8b9d51e-295d-4535-9c2c-cacb35120ccf)

</details>

<details>

<summary><strong>Audit</strong>: for the audit module functions</summary>

Endpoint about the documents to check :\
[/api/audit/documents-to-manage](https://documenter.getpostman.com/view/30765019/2s9YXcek45#402f9e1c-996b-4f19-99b4-c225743d12c5)

Endpoints about the duplicates :\
[/api/audit/duplicated-information\
](https://documenter.getpostman.com/view/30765019/2s9YXcek45#d031937a-1d85-4ad5-a8ad-63dbff856d11)[/api/audit/duplicated-information/set-managed](https://documenter.getpostman.com/view/30765019/2s9YXcek45#92375790-3e7d-42f8-b342-c499e2697589)

Endpoints about the conflicts :\
[/api/audit/conflict-information\
](https://documenter.getpostman.com/view/30765019/2s9YXcek45#402f9e1c-996b-4f19-99b4-c225743d12c5)[/api/audit/conflict-information/set-managed](https://documenter.getpostman.com/view/30765019/2s9YXcek45#63769552-ac77-4f67-9d4f-fab70dce6f12)

Endpoint about the missing informations from your users inquiries :\
[/api/audit/missing-subjects](https://documenter.getpostman.com/view/30765019/2s9YXcek45#8b07ae67-eaaa-4525-bd23-d0c6c85123cf)

</details>

<details>

<summary><strong>Search</strong> : for search module functions</summary>

Endpoints about the queries :\
[/api/search/query\
](https://documenter.getpostman.com/view/30765019/2s9YXcek45#671e7562-0469-49e1-bb08-8636af1279f5)[/api/search/identify-specific-document](https://documenter.getpostman.com/view/30765019/2s9YXcek45#d08fad38-133c-4e7b-ab69-284e67a1565e)

Endpoints about the statistics of the queries :\
[/api/search/stats/list-search](https://documenter.getpostman.com/view/30765019/2s9YXcek45#8f2da3a5-7189-49b7-a974-d95673220148)\
[/api/search/stats/count-search](https://documenter.getpostman.com/view/30765019/2s9YXcek45#971d29f8-9759-46e4-a196-746cf8ac9438)\
[/api/search/stats/count-answered-search](https://documenter.getpostman.com/view/30765019/2s9YXcek45#a3f7a313-3a20-4c97-aa40-32ba5e5bbe8e)

Endpoints about the documents available :\
[/api/search/docs](https://documenter.getpostman.com/view/30765019/2s9YXcek45#8b256aef-d186-446c-ae04-888ea2801cb9)\
[/api/search/doc](https://documenter.getpostman.com/view/30765019/2s9YXcek45#feaba1ad-8bfa-4433-954b-85c346dd356f)

</details>

<details>

<summary><strong>Semantic Graph</strong>: for raw results related to graph generation from provided documents</summary>

Endpoints about the semantic nodes :\
[/api/semantic-graph/nodes](https://documenter.getpostman.com/view/30765019/2s9YXcek45#d42106e8-cb39-4ef1-9106-e13b71b76c5c)\
[/api/semantic-graph/linked-nodes](https://documenter.getpostman.com/view/30765019/2s9YXcek45#811547e7-b9b0-4299-b3f1-2d9eb5e17cf9)\
[/api/semantic-graph/nodes-by-label](https://documenter.getpostman.com/view/30765019/2s9YXcek45#cc189b46-fabd-4695-b7c5-6cf6c9b0364e)\
[/api/semantic-graph/identify-nodes](https://documenter.getpostman.com/view/30765019/2s9YXcek45#7fcf3cee-611c-4429-ac3e-31c8fc29f100)

</details>

