# 1Password Connect Terraform Provider

Use the 1Password Connect Terraform Provider to reference, create, or update items in your 1Password Vaults.

## Building

To build the 1Password Connect Terraform provider run the following

```sh
$ go build .
```

This will create the `terraform-provider-onepassword` binary

## Testing the Provider

To run the go tests and check test coverage run the following

```sh
$ go test -v ./... -cover
```

## Installing Locally

To install the binary it must be copied to the appropriate terraform plugin directory. You may need to create the appropriate directories. For more information [see these Terraform 0.13 plugin docs](https://www.hashicorp.com/blog/automatic-installation-of-third-party-providers-with-terraform-0-13)

The current version of the provider is considered to be 0.1 and `darwin_amd64` should match your machines operating system and architecture in the format `$OS_$ARCH`. For example macOS is `darwin_amd64` and linux is `linux_amd64`.

```sh
$ mkdir -p ~/.terraform.d/plugins/github.com/1Password/onepassword/0.1/darwin_amd64/
$ cp ./terraform-provider-onepassword ~/.terraform.d/plugins/github.com/1Password/onepassword/0.1/darwin_amd64/terraform-provider-onepassword
```

## Using plugin locally

In your Terraform configuration you will need to specify the op plugin with

```tf
terraform {
  required_providers {
    onepassword = {
      version = "0.1"
      source   = "github.com/1Password/onepassword"
    }
  }
}

provider "onepassword" {
  url     = "http://<1Password Connect API Hostname>"
}
```

After copying a newly built version of the provider to the plugins directory you will have to run `terraform init` again. If you forget to do this terraform will error out and tell you to do so.