---
title: "Top 10 terraform tools you should know about."
source: "https://dev.to/digger/top-10-terraform-tools-you-should-know-about-1fhg"
author:
  - "[[Utpal Nadiger]]"
published: 2023-12-11
created: 2025-02-17
description: "Terraform stands out as a powerful Infrastructure-as-Code (IaC) tool on its own, yet as the... Tagged with devops, terraform, infrastructureascode, opensource."
tags:
  - "clippings"
---
Terraform stands out as a powerful Infrastructure-as-Code (IaC) tool on its own, yet as the sophistication of your infrastructure grows, you might discover the need for additional tooling for specific use-cases.

In this article, we will explore some of the leading tools currently employed in deployments managed by Terraform.

Let's dive right in 👇

## Digger

[Digger](https://github.com/diggerhq/digger) is an Open Source IaC management platform that allows you to orchestrate terraform/OpenTofu in your CI/CD system. It helps you resue async jobs infrastructure with compute, orchestration, logs, etc of your existing CI. Digger also has a pro version built on top of Digger’s community edition. Digger’s “bring your own compute” ensures that users have private runners by defualt and don’t have to pay for it additionally. Digger pro gives team leads, managers and IaC practitioners dashboards, Drift Detection, RBAC via OPA policies and concurrency so they can help guide the team.

[![Digger - an open source IaC management tool](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Foru9smchzyah4xw4m1cv.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Foru9smchzyah4xw4m1cv.png)

[Star Digger on GitHub ⭐️](https://github.com/diggerhq/digger)

## Checkov

[Checkov](https://github.com/bridgecrewio/checkov) is a versatile static code analysis tool designed for infrastructure as code (IaC) and software composition analysis (SCA). It supports a wide range of technologies, including Terraform, CloudFormation, Kubernetes, Docker, and others, to detect security and compliance issues through graph-based scanning. Checkov also performs SCA scans, identifying vulnerabilities in open source packages and images by checking for Common Vulnerabilities and Exposures (CVEs). Additionally, it is integrated into Prisma Cloud Application Security, a platform that helps developers secure cloud resources and infrastructure-as-code files, enabling the identification, rectification, and prevention of misconfigurations throughout the development lifecycle.

[Star Checkov on GitHub ⭐️](https://github.com/bridgecrewio/checkov)

## Former2

[Former2](https://github.com/iann0036/former2) is a tool that automates the creation of Infrastructure-as-Code (IaC) scripts from existing AWS resources. It utilizes the AWS JavaScript SDK to scan the user’s AWS infrastructure, identifying all available resources. Users can then select from this list which resources they want to include in their IaC outputs. This process simplifies the task of writing IaC scripts, especially for complex environments, by directly converting current AWS configurations into ready-to-use code. Former2 is particularly useful for documenting existing infrastructure or for migrating manually created resources into an IaC framework.

[Star Former2 on GitHub ⭐️](https://github.com/iann0036/former2)

## Infracost

[Infracost](https://github.com/infracost/infracost) is a tool that provides cloud cost estimates for infrastructure managed by Terraform. It enables engineers to view and understand the financial impact of their infrastructure changes before they are applied. Infracost integrates directly into the workflow, offering cost breakdowns in various environments like the terminal, Visual Studio Code, or directly within pull requests. This feature allows for more informed decision-making regarding infrastructure modifications, promoting cost-awareness and budget management in the early stages of development. Infracost is particularly useful for teams looking to balance cloud resource utilization with budget constraints. Infracost Cloud is their SaaS product that builds on top of Infracost open source and works with CI/CD integrations. It gives team leads, managers and FinOps practitioners dashboards, guardrails, centralized cost policies and Jira integration so they can help guide the team (e.g. switch AWS GP2 volumes to GP3).

[![Infracost](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Flafkweu9m9tkj7vf8n9s.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Flafkweu9m9tkj7vf8n9s.png)

[Star Infracost on GitHub ⭐️](https://github.com/infracost/infracost)

## Terragrunt

Created and maintained by Gruntwork, [Terragrunt](https://github.com/gruntwork-io/terragrunt) is a tool designed to enhance Terraform’s capabilities. It acts as a thin wrapper around Terraform, offering additional features to streamline and optimise Terraform usage. Key functions of Terragrunt include helping users keep their Terraform configurations DRY (Don’t Repeat Yourself), efficiently managing multiple Terraform modules, and handling remote state management. By reducing repetition in Terraform code and simplifying the management of complex module dependencies and remote state, Terragrunt makes working with Terraform more efficient, especially for larger or more complex infrastructure deployments.

[![Terragrunt](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fap0jaw3516jowramzn9m.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fap0jaw3516jowramzn9m.png)

[Star Terragrunt on GitHub ⭐️](https://github.com/gruntwork-io/terragrunt)

## Sato

[Sato](https://github.com/JamesWoolfenden/sato) is a conversion tool designed to translate CloudFormation and ARM (Azure Resource Manager) templates into Terraform configurations. Developed in Go, Sato stands out for its speed and efficiency in this conversion process. By automating the translation of existing templates into Terraform’s syntax, Sato facilitates a smoother and quicker migration to Terraform’s ecosystem.

[Star Sato on GitHub ⭐️](https://github.com/JamesWoolfenden/sato)

## Prettyplan

[Prettyplan](https://prettyplan.chrislewisdev.com/) is a user-friendly tool designed to simplify the review of large Terraform plan outputs. It enhances readability by providing an online interface where users can paste their Terraform plan output, which is then reorganized into a more manageable format. Key features include expandable and collapsible sections for a comprehensive yet detailed view, a tabular layout for straightforward comparison of old and new values, and improved display formatting for multi-line strings like JSON documents. Initially created for Terraform versions up to 0.11, Prettyplan’s relevance has diminished with Terraform’s 0.12 update, which incorporated many of Prettyplan’s functionalities, leading to no further updates for the tool.

[Star Pretty Plan on GitHub ⭐️](https://github.com/chrislewisdev/prettyplan)

## Regula

[Regula](https://github.com/fugue/regula) is a dynamic tool designed for pre-deployment security and compliance checks of infrastructure as code (IaC) for multiple cloud providers and Kubernetes. It supports an array of file types, including CloudFormation JSON/YAML templates, Terraform source code and JSON plans, Kubernetes YAML manifests, and Azure Resource Manager (ARM) JSON templates (currently in preview). Regula leverages a rule library written in Rego, the language used by the Open Policy Agent (OPA) project, offering robust policy evaluation. It integrates seamlessly with popular CI/CD tools like Jenkins, Circle CI, and AWS CodePipeline, and even includes a GitHub Actions example for easy setup. Regula’s policies are aligned with CIS Benchmarks for AWS, Azure, Google Cloud, and Kubernetes, aiding in comprehensive compliance assessments. This tool is actively developed and maintained by the team at Fugue.

[Star Regula on GitHub ⭐️](https://github.com/fugue/regula)

## Terraboard

[Terraboard](https://terraboard.io/) is a web-based dashboard designed for visualizing and querying Terraform states. It offers several key features: an overview page that lists the most recently updated state files along with their activities; a detailed state page showing versions and resource attributes of state files; a search interface for querying resources by type, name, or attributes; and a diff interface for comparing state versions. Terraboard supports various remote state backend providers, including AWS S3 for state management and DynamoDB for locking, S3-compatible backends like MinIO, Google Cloud Storage, Terraform Cloud (remote), and GitLab. This makes it a versatile tool for managing and understanding Terraform state files.

[![Terraboard](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fx3pysfoq9rulkk3xwkhy.png)](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fx3pysfoq9rulkk3xwkhy.png)

[Star Terraboard on GitHub ⭐️](https://github.com/camptocamp/terraboard%3Cbr%3E%0A)

## TFLint

[TFlint](https://github.com/terraform-linters/tflint) is a powerful linter for Terraform, designed to catch errors and issues that `terraform plan` may not detect. As Terraform grows in popularity for infrastructure as code, the need for robust tools to ensure code quality and reliability becomes paramount. TFlint fulfills this need by analyzing Terraform configurations to find problems that are not covered by syntax checks. It checks for things like unsuitable AWS instance types, incorrect IAM policy syntax, and the use of deprecated syntax or features. By integrating TFlint into the development process, users can proactively identify potential problems, improving the stability and efficiency of their infrastructure deployments. This additional layer of validation is crucial for maintaining high standards in complex, cloud-based infrastructures.

[Star TFLint on GitHub ⭐️](https://github.com/terraform-linters/tflint)

*This article was orginally published on medium - link [here](https://medium.com/@DiggerHQ/10-terraform-tools-you-should-know-about-0dfd9862fae8)*