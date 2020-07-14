# RTMP Server

Terraform module which create RTMP proxy using nginx.

RTMP is a video streaming protocol that makes high quality live streaming possible. This server enables the splitting of the RTMP stream to multiple locations (Facebook, YouTube (but you could add others (Twitch/Ustream)).

## Usage

### `main.tf`

```hcl
module "rtmp" {
  source       = "./modules/rtmp_server"
  youtube_key  = var.youtube_key
  facebook_key = var.facebook_key
  key_name     = var.keyname
}
```

### `variables.tf`

```hcl
variable youtube_key {
  description = "YouTube RTMP key"
  default     = ""
  required    = true
}

variable facebook_key {
  description = "Facebook RTMP key"
  default     = ""
  required    = true
}

variable keyname {
  description = "SSH Keyname (for SSH access if required)."
  default     = ""
}
```

### `outputs.tf`

```hcl
output "ip_address" {
  description = "External IP address to route"
  value = module.rtmp.ip_address
}
```

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| aws | n/a |
| cloudinit | n/a |
| template | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| facebook\_key | Facebook RTMP Stream Key | `string` | n/a | yes |
| youtube\_key | YouTube RTMP Stream Key | `string` | n/a | yes |
| instance\_type | EC2 instance type | `string` | `"t2.micro"` | no |
| key\_name | n/a | `string` | `"keyname"` | no |
| nginx\_rtmp\_version | RTMP Module for nginx installation version https://github.com/arut/nginx-rtmp-module | `string` | `"1.2.1"` | no |
| nginx\_version | Version of nginx for installation (nginx-\*). | `string` | `"nginx-1.18.0"` | no |
| project\_tags | Project tags to be used to track costs. | `map(string)` | <pre>{<br>  "Name": "RTMP-Restreamer",<br>  "Owner": "Will Hall Online",<br>  "Purpose": "Live streaming"<br>}</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| ip\_address | External IP address for routing RTMP traffic |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
