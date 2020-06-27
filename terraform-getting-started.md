# Getting Started With Terraform

Terraform is the most popular language for defining and provisioning infrastructure as code (IaC). Terraform is also a tool for building, changing, and managing infrastructure in a safe, repeatable way. Operators and infrastructure teams can use Terraform to manage environments with a configuration language called the HashiCorp Configuration Language (HCL) for human-readable, automated deployments.

In this tutorial, you will learn how to install Terraform on the AWS platform, build infrastructure, initialize Terraform, and destroy infrastructure.

See [Introduction to Infrastructure as Code with Terraform](https://learn.hashicorp.com/terraform/getting-started/intro) for more on infrastructure as code, deployment workflows, and the advantages of Terraform. 

## Prerequisites
To follow this tutorial, you will need:
- An AWS account
- The [AWS CLI](https://kubernetes.io/docs/tasks/tools/install-kubectl/) client installed
- Your AWS credentials configured locally
- A Docker account

## Install Terraform on the AWS Platform

To install Terraform, visit [Terraform.io](https://www.terraform.io/downloads.html) and download the executable file needed for your system.

After downloading Terraform, unzip the package. Terraform runs as a single binary named `terraform`. Any other files in the package can be safely removed, and Terraform will still function. (You can also compile the Terraform binary from source.)

Finally, make sure that the terraform binary is available on your PATH. This process will differ depending on your operating system.

Click [here](https://learn.hashicorp.com/terraform/getting-started/install) for troubleshooting tips and more information on how to install Terraform.

## Build Infrastructure

With Terraform installed, you can start creating infrastructure.

### Create New Directory

First, create a new directory on your local machine where you will save your Terraform configuration code file. Each configuration should be in its own directory.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

### Create a Terraform Configuration Code File

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
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
Click [here](https://learn.hashicorp.com/terraform/getting-started/build) for more information on how to build infrastructure.

## Initialize Terraform

Initialize Terraform with the `init` command. The AWS provider will then be installed. 

```shell
$ terraform init
```

If the `init` ran successfully, then provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take a few minutes to run and will display a message indicating that the resource was created.

## Destroy Infrastructure

Finally, destroy the infrastructure.

```shell
$ terraform destroy
```

Look for a message at the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it created earlier.

Click [here](https://learn.hashicorp.com/terraform/getting-started/destroy) for more information on destroying infrastructure.

## Next Steps

Now that you have learned how to install and initialize Terraform, as well as build and destroy infrastructure, continue to the next tutorial in this track to on [resource dependencies](https://learn.hashicorp.com/terraform/getting-started/dependencies), where you will not only see a configuration with multiple resources for the first time, but also scenarios where resource parameters use information from other resources.

Here are more resources and information that you may find helpful:

- Read about the format of the configuration files in the [Terraform documentation](https://www.terraform.io/docs/configuration/index.html).
- Review this [blog post](https://aws.amazon.com/blogs/apn/terraform-beyond-the-basics-with-aws/) to go beyond the basics with Terraform and AWS.
- Sign up for this [webinar](https://www.hashicorp.com/webinars/improved-workflows-with-terraform/) on improving workflows with Terraform 0.13.


