# Getting Started with Terraform

Terraform is a popular language for defining and provisioning infrastructure as code (IaC). In this guide, you will learn how to configure your first Terraform IaC file using the `init`, `apply`, and `destroy` commands.

## Prerequisites

- The [Terraform CLI](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started) installed
- [Docker](https://docs.docker.com/get-docker/) installed


## Quick start configuration

With Terraform installed, you will now provision an NGINX resource in Docker.  

Create a new directory using `mkdir` and then navigate into it using `cd`.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the `main.tf` file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Initialize Terraform with the `init` command so Terraform can interact with Docker.

```shell
$ terraform init
```

Provision the NGINX resource with the `apply` command. Next, Terraform will ask for confirmation, type `yes` and press `ENTER`. The `apply` command may take a few minutes to run and will display a message indicating that the resource was created.

```shell
$ terraform apply
```

Finally, destroy the infrastructure with the `destroy` command. Terraform will ask for confirmation, type `yes` and press `ENTER`. 

```shell
$ terraform destroy
```

You have successfully configured, provisioned, and destroyed an NGINX resource in Docker with Terraform. 

## Next Steps

Next, you can continue to build infrastructure in [Docker](https://learn.hashicorp.com/collections/terraform/docker-get-started) or you can start building in your chosen cloud platform.

- [Amazon Web Services (AWS)](https://learn.hashicorp.com/tutorials/terraform/aws-build?in=terraform/aws-get-started)
- [Google Cloud Platform (GCP](https://learn.hashicorp.com/collections/terraform/gcp-get-started)
- [Microsoft Azure](https://learn.hashicorp.com/collections/terraform/azure-get-started)
- [Oracle Cloud Infrastructure (OCI)](https://learn.hashicorp.com/collections/terraform/oci-get-started)

