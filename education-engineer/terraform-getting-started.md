# Getting Started with Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC).

To install Terraform, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the applicable binary package for your operating system or use your favorite package management system to install the Terraform package. The [Install Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli?in=terraform/aws-get-started) page has additional tutorials for installing Terraform.

After you install Terraform on your local machine, create a new directory and then navigate into it.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the 'main.tf' file.

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

Initialize Terraform with the `init` command to interact with Docker.

```shell
$ terraform init
```

Provision the NGINX resource with the `apply` command. Next, Terraform will ask for confirmation, type 'yes' and press 'ENTER'.

```shell
$ terraform apply
```

The 'apply' command will take up to a few minutes to run and will display a message indicating that the resource was created.

Finally, destroy the infrastructure with the 'destroy' command. Terraform will ask for confirmation, type 'yes' and press 'ENTER'. 

```shell
$ terraform destroy
```

You have successfully provisioned and destroyed an NGINX resource with Terraform. 
