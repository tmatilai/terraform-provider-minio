---
page_title: "Provider: Minio"
description: Manage Minio with Terraform.
---

# Minio Provider

This is a terraform provider plugin for managing [Minio](https://min.io/) S3 buckets and IAM users.

## Example Provider Configuration

```terraform
provider minio {
  // required
  minio_server   = "..."
  minio_user     = "..."
  minio_password = "..."

  // optional
  minio_session_token = "..."
  minio_region        = "..."
  minio_api_version   = "..."
  minio_ssl           = "..."
  minio_insecure      = "..."
}
```

## Authentication

The Minio provider offers the following methods of providing credentials for
authentication, in this order, and explained below:

- Static API key
- Environment variables

### Static API Key

Static credentials can be provided by adding the `minio-server`, `minio_user` and `minio_password` variables in-line in the
Minio provider block:

Usage:

```hcl
provider "minio" {
  minio_server   = "..."
  minio_user     = "..."
  minio_password = "..."
}
```

### Environment variables

You can provide your configuration via the environment variables representing your minio credentials:

```
export MINIO_ENDPOINT="http://myendpoint"
export MINIO_ROOT_USER="244tefewg"
export MINIO_ROOT_PASSWORD="xgwgwqqwv"
```

When using this method, you may omit the
minio `provider` block entirely:

```hcl
resource "minio_s3_bucket" "state_terraform_s3" {
  # .....
}
```

## Argument Reference

The following arguments are supported in the `provider` block:

- `minio_server` - (Required) Minio Host and Port. It must be provided, but
  it can also be sourced from the `MINIO_ENDPOINT` environment variable

- `minio_user` - (Required) Minio User. It must be provided, but
  it can also be sourced from the `MINIO_USER` environment variable

- `minio_password` - (Required) Minio Password. It must be provided, but
  it can also be sourced from the `MINIO_PASSWORD` environment variable

- `minio_session_token` - (Optional) Minio Session Token. It can also be sourced from
  the `MINIO_SESSION_TOKEN` environment variable

- `minio_region` - (Optional) Minio Region (`default: us-east-1`).

- `minio_api_version` - (Optional) Minio API Version (type: string, options: `v2` or `v4`, default: `v4`).

- `minio_ssl` - (Optional) Minio SSL enabled (default: `false`). It can also be sourced from the
  `MINIO_ENABLE_HTTPS` environment variable

- `minio_insecure` - (Optional) Disable SSL certificate verification (default: `false`).
  It can also be sourced from the `MINIO_INSECURE` environment variable.
