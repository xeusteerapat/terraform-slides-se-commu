---
# try also 'default' to start simple
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# some information about your slides, markdown enabled
title: Introduction to Terraform
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
---

# Introduction to Terraform

## SE Community 2024
by
### Teerapat Prommarak


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: image-right
image: ./infra-as-code.png
---

# What is Infrastructure as Code?

- Practice of managing and provisioning computing infrastructure through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.

- Automated provisioning, configuration, and management of infrastructure resources.

- IaC enables consistency, scalability, and repeatability in infrastructure deployment and management processes.

---
layout: image-right
image: ./terraform.avif
---
<style>
@import './style.css';
</style>

# Overview of Terraform

- **Terraform** is an open-source infrastructure as code software tool created by HashiCorp.
  
- It enables users to define and provision infrastructure using a high-level configuration language known as **HashiCorp Configuration Language** (HCL).

- **Terraform** allows for the management of infrastructure across various cloud providers (such as AWS, Azure, Google Cloud) as well as on-premises environments.

---


# Terraform Basics

- **Declarative vs. Imperative Approach**: Terraform follows a declarative approach, where you define the desired state of your infrastructure, rather than specifying the exact steps to achieve it.

- **Terraform Configuration Language (HCL)**: HCL is a simple, human-readable language used to define Terraform configurations. It allows you to describe infrastructure components and their relationships.

- **Infrastructure Management**: Terraform manages infrastructure resources through the use of providers and resources. Providers are responsible for managing the lifecycle of resources provided by a specific cloud or service.

---

# Basic Terraform Syntax

<div class="grid grid-cols-2 gap-4">

<div>

### Variable Declaration

```hcl
variable "service_name" {
  description = "The name of the Cloud Run service"
  type        = string
}

variable "region" {
  description = "The region where service will be deployed"
  type        = string
}
```

### Resource Block

```hcl
resource "aws_instance" "example" {
  ami           = var.image_id
  instance_type = "t2.micro"
}
```
</div>
<div>

### Loop (Count)

```hcl
variable "users" {
  type = map(object({
    role = string
  }))
}
 
locals {
  users_by_role = {
    for name, user in var.users : user.role => name...
  }
}
```

### Object

```hcl
variable "tags" {
  type = map(string)
  default = {
    Name    = "example-instance"
    Owner   = "user"
    Project = "demo"
  }
}
```
</div>
</div>
---


# Terraform Architecture

- **Components**: Terraform architecture consists of several components, including providers, resources, state files, and modules. Providers are responsible for interacting with APIs of various cloud providers.

- **Provider Plugins**: Terraform uses provider plugins to interface with different cloud providers. These plugins abstract the underlying API calls and provide a consistent interface for managing resources.

- **State Management**: Terraform maintains a state file that records the current state of your infrastructure. This state file is used to track the relationship between your configuration and the real-world infrastructure.

---
level: 2
---

# Getting Started with Terraform

- **Installation and Setup**: Install Terraform CLI, initialize a new project with `terraform init`.

- **Writing Your First Configuration**: Create a `.tf` file, declare provider and resources.

- **Common Commands**: Use `terraform plan` to preview changes, `terraform apply` to apply changes, and `terraform destroy` to remove resources.

---

# Terraform Workflow

- **Initialize (`terraform init`)**: Initializes a Terraform working directory then sets up the backend configuration and downloads the provider plugins required for the configuration.

- **Validation (`terraform validate`)**: Checks the syntax and internal consistency of the configuration files without making any changes to the infrastructure.

- **Planning (`terraform plan`)**: Generate an execution plan showing what Terraform will do when you apply your configuration. It helps you understand the changes that Terraform will make to your infrastructure.

- **Applying Changes (`terraform apply`)**: Apply the changes described in the Terraform configuration to your infrastructure. Terraform will create, update, or delete resources as necessary to match the desired state.

- **Destroying Resources (`terraform destroy`)**: Destroy the resources defined in your Terraform configuration. Use with caution as it permanently deletes infrastructure resources.

---

# Terraform Modules

- **Modular Infrastructure**: Modularize your Terraform configurations for reusable and scalable infrastructure components.

- **Create or Reuse**: Build your own modules or leverage existing ones from the Terraform Registry.

- **Best Practices**: Follow naming conventions, versioning, and documentation for organized and maintainable modules.

---

# Terraform Modules

```shell
terraform/
├── modules/
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── ...
│   └── ...
├── dev/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── ...
├── uat/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   └── ...
└── prod/
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf
    └── ...
```

---
layout: image-right
image: ./tf-providers.png
---

# Terraform Providers

- **Plugin-based Integration**: Providers in Terraform abstract APIs of various cloud services for resource management.

- **Configure Easily**: Use `provider` blocks to configure authentication and other settings for interacting with provider APIs.

- **Wide Support**: Terraform supports major cloud providers like AWS, Azure, Google Cloud, and more, offering resources specific to each.

---

# Terraform State Management

- **Track Infrastructure State**: Terraform maintains a state file to track the current state of your infrastructure.

- **Local and Remote State**: Manage state locally or store it remotely for collaboration and consistency.

- **State Locking**: Prevent concurrent state modifications with state locking mechanisms.

---

# Terraform Best Practices

- **Modular Code**: Organize infrastructure into reusable modules.
- **Version Control**: Use version control systems (e.g., Git) to track changes and collaborate.
- **State Management**: Use remote state for team collaboration and backup.
- **Naming Conventions**: Follow consistent naming conventions for resources.
- **Documentation**: Document your configurations and modules for clarity.

---

# Terraform vs Other IaC Tools

- **Pulumi**:
  - **Language**: Supports multiple programming languages (JavaScript, TypeScript, Python, Go, .NET)
  - **Providers**: Wide support, similar to Terraform
  - **Community**: Growing community, rich ecosystem for multi-language support

- **AWS CDK / Terraform CDK**:
  - **Language**: Supports multiple programming languages (TypeScript, JavaScript, Python, Java, C#)
  - **Providers**: Primarily focused on AWS (AWS CDK), multi-cloud support (Terraform CDK)
  - **Community**: Strong AWS community, growing CDK community

---

# References

- https://developer.hashicorp.com/terraform
- https://aws.amazon.com/what-is/iac/?nc1=h_ls

---
layout: center
---

# Demo

<img src="/google_cloud_run_architecture.png" alt="GCP Cloud Run" style="width: 450px; height: 450px;" />
