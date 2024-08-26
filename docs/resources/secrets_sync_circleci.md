---
page_title: "doppler_secrets_sync_circleci Resource - terraform-provider-doppler"
subcategory: ""
description: |-
	Manage a CircleCI Doppler sync.
---

# doppler_secrets_sync_circleci (Resource)

Manage a CircleCI Doppler sync.

## Example Usage

```terraform
resource "doppler_integration_circleci" "prod" {
  name      = "Production"
  api_token = "my_api_token"
}

resource "doppler_secrets_sync_circleci" "backend_prod" {
  integration = doppler_integration_circleci.prod.id
  project     = "backend"
  config      = "prd"

  resource_type     = "project"
  resource_id       = "github/myorg/myproject"
  organization_slug = "myorg"

  delete_behavior = "leave_in_target"
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Required

- `config` (String) The name of the Doppler config
- `integration` (String) The slug of the integration to use for this sync
- `organization_slug` (String) The organization slug where the resource is located
- `project` (String) The name of the Doppler project
- `resource_id` (String) The resource ID (either project or context) to sync to
- `resource_type` (String) Either "project" or "context", based on the resource type to sync to

### Optional

- `delete_behavior` (String) The behavior to be performed on the secrets in the sync target when this resource is deleted or recreated. Either `leave_in_target` (default) or `delete_from_target`.

### Read-Only

- `id` (String) The ID of this resource.