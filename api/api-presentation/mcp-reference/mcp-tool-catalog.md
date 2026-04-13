---
description: >-
  A compact reference of every MCP tool KAI exposes, with links to the full
  endpoint documentation.
---

# MCP tool catalog

### Retrieval MCP (stable)

Server: `https://api-retrieval.kai-studio.ai/mcp`

| Tool (`operation_id`)                          | Endpoint page  | Description                                          |
| ---------------------------------------------- | -------------- | ---------------------------------------------------- |
| `retrieval_instances_list_available_instances` | Instances      | List accessible instances with composed instructions |
| `retrieval_documents_list`                     | Documents      | Paginated list of documents in an instance           |
| `retrieval_documents_get_document`             | Documents      | Fetch the full content of one document               |
| `retrieval_documents_list_by_ids`              | Documents      | Fetch multiple documents by ID in a single call      |
| `retrieval_semantic_nodes_search`              | Semantic nodes | Semantic search across a knowledge base              |

### Audit MCP (BETA)

Server: `https://api-audit.kai-studio.ai/mcp`

| Tool (`operation_id`)                                | Endpoint page          | Description                                                         |
| ---------------------------------------------------- | ---------------------- | ------------------------------------------------------------------- |
| `audit_instance_list_for_user`                       | Instances              | List all audit instances accessible by the authenticated user       |
| `audit_instance_get`                                 | Instances              | Retrieve detailed information for a specific audit instance         |
| `audit_instance_get_kai_instances`                   | Instances              | List all KAI document instances linked to an audit instance         |
| `audit_instance_delete_kai_instance`                 | Instances              | Remove a KAI document instance from an audit instance               |
| `audit_instance_add_kai_instance`                    | Instances              | Link a new KAI document instance to an audit instance               |
| `audit_instance_update_step`                         | Instances              | Update the current workflow step of an audit instance               |
| `audit_instance_update_configuration`                | Instances              | Update the configuration settings of an audit instance              |
| `audit_document_list`                                | Documents & indexation | List documents for an audit instance with pagination                |
| `audit_document_set_owner`                           | Documents & indexation | Assign or unassign an owner to a document                           |
| `audit_duplicate_list`                               | Duplicates             | List duplicate document clusters for an audit instance              |
| `audit_duplicate_set_managed`                        | Duplicates             | Mark a duplicate cluster as managed                                 |
| `audit_mandatory_question_list`                      | Mandatory questions    | List mandatory questions with optional state filtering              |
| `audit_mandatory_question_create`                    | Mandatory questions    | Create a new mandatory question for an audit instance               |
| `audit_mandatory_question_set_answer`                | Mandatory questions    | Set or update the answer for a mandatory question                   |
| `audit_mandatory_question_set_managed`               | Mandatory questions    | Mark a mandatory question as managed and trigger reindexation       |
| `audit_mandatory_question_set_ignored`               | Mandatory questions    | Mark a mandatory question as ignored                                |
| `audit_mandatory_question_generate_compagnon_answer` | Mandatory questions    | Generate an AI companion recommendation for a mandatory question    |
| `audit_mandatory_question_force_analyze`             | Mandatory questions    | Force re-analysis of a refused mandatory question                   |
| `audit_full_audit_have_to_show`                      | Questions & answers    | Check whether the full audit view should be displayed               |
| `audit_full_audit_get_detail`                        | Questions & answers    | Retrieve detailed information for a full audit conflict             |
| `audit_full_audit_set_expert_answer`                 | Questions & answers    | Set an expert answer for a full audit conflict                      |
| `audit_conflict_list`                                | Conflicts              | List all conflicts for an audit instance with pagination            |
| `audit_conflict_get`                                 | Conflicts              | Retrieve detailed information for a specific conflict               |
| `audit_conflict_set_answer`                          | Conflicts              | Set or update the audit answer for a conflict                       |
| `audit_conflict_get_top_collaborators`               | Conflicts              | Get the top collaborators sharing conflicts with the current user   |
| `audit_missing_subject_list`                         | Missing subjects       | List missing subjects for an audit instance                         |
| `audit_missing_subject_find`                         | Missing subjects       | Retrieve detailed information for a specific missing subject        |
| `audit_missing_subject_list_questions`               | Missing subjects       | List all questions associated with a missing subject                |
| `audit_missing_subject_set_state`                    | Missing subjects       | Update the state of a missing subject                               |
| `audit_missing_subject_generate_compagnon_document`  | Missing subjects       | Generate an AI companion document proposition for a missing subject |
| `audit_stats_get_daily`                              | Stats                  | Retrieve daily audit statistics for an instance                     |
| `audit_stats_get_user`                               | Stats                  | Retrieve audit statistics for a specific user                       |
| `audit_stats_get_filtered`                           | Stats                  | Retrieve aggregated audit statistics filtered by document owner     |
| `audit_user_get_users`                               | Instances              | List all users associated with an audit instance                    |
| `audit_user_list_instances`                          | Instances              | List all audit instances for a user within an organization          |
| `audit_user_add`                                     | Instances              | Add a user to an audit instance                                     |
| `audit_user_remove`                                  | Instances              | Remove a user from an audit instance                                |
| `audit_user_set_admin`                               | Instances              | Promote a user to admin role for an audit instance                  |
| `audit_user_set_normal`                              | Instances              | Demote a user to regular role for an audit instance                 |
| `audit_user_is_admin`                                | Instances              | Check whether the user has admin privileges for an audit instance   |
