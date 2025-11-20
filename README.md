# Cloud Infrastructure Portfolio - Project Root
[![License](https://img.shields.io/badge/license-CC%20BY--SA%204.0-blue.svg)](LICENSE) [![Portfolio Tag](https://img.shields.io/badge/tag-cip--project--root-orange.svg)](#) [![AWS SAA-03](https://img.shields.io/badge/certification-AWS%20SAA--03-brightgreen.svg)](#)


## Introduction

`cip_project-root` is the root hub for the **Cloud Infrastructure Portfolio (CIP)** — a curated collection of realistic, production-oriented AWS and Infrastructure-as-Code projects. This repository holds central documentation, architecture overviews, conventions, and links (via Git submodules) to each project repository.

This repo is intended to:

* Provide a single, well-organized entry point to all CIP projects.
* Host architecture diagrams, portfolio-level standards, and contributor guidance.
* Include *project folders* (with local docs and links) that point to independent Git repos (submodules) containing the actual code and IaC.

License: This collection is released under the **GNU General Public License Version 3 (GPL-3.0) License** — see `LICENSE` for details.

<br/>


## Table of contents

1. [Project structure](#project-structure)
2. [Projects (overview)](#projects-overview)

   * [Minecraft Server (EC2 Spot + fallback)](#minecraft-server-ec2-spot--fallback)
   <!-- * [Terraform VPC & Networking module](#terraform-vpc--networking-module)
   * [CI/CD — CodePipeline / GitHub Actions examples](#cicd--codepipeline--github-actions-examples)
   * [Container platform — ECS / Fargate & EKS samples](#container-platform--ecs--fargate--eks-samples)
   * [Static site — S3 + CloudFront pipeline](#static-site--s3--cloudfront-pipeline)
   * [Monitoring & Observability (CloudWatch + Grafana)](#monitoring--observability-cloudwatch--grafana)
   * [Home / Office Intranet Lab (networking + PoE)](#home--office-intranet-lab-networking--poe) -->
3. [Standards & conventions](#standards--conventions)
4. [How to use submodules](#how-to-use-submodules)
5. [Contributing](#contributing)
6. [Credits & Attribution](#credits--attribution)

<br/>


## 1. Project structure

```text
cip_project-root/
├─ Docs/                              # Portfolio-level diagrams and notes
│  └─ Diagrams/                       # PNG/SVG/PlantUML files
├─ Standards/                         # IaC style, naming conventions, CI templates
├─ Projects/                          # Local folders for each project (docs + submodule pointers)
│   ├─ CIP-001: Static site on S3/    # README + link to submodule (git submodule)
│   │  ├─ Docs/                       # Portfolio-level diagrams and notes
│   │  │  └─ Diagrams/                # PNG/SVG/PlantUML files
│   │  ├─ Project submodules...       # A submodule for each of the repositories that makes the project.
│   │  └─ README.md                   # Detailed project description.
│   └─ Other projects...
├─ LICENSE                            # License these projects fall under.
└─ README.md                          # This file
```

Each folder under `projects/` should contain at minimum a `README.md` describing the project, a short architecture diagram, and a file (or README section) that explains which remote repository is linked as a submodule.

<br/>


## 2. Projects (overview)

> Each entry below links to the corresponding folder in this repository (local docs). The actual implementation lives in the submodule repository linked from each folder's README.

### [CIP-001: Static site — S3 & CloudFront pipeline](https://github.com/MHooijberg/cip_project-root/projects)

**Folder:** `projects/cip-001_static-site-on-s3/`

**Idea:** Host a static portfolio site on S3 with CloudFront, automatic invalidation, TLS, and a CI pipeline that builds and deploys the site. Demonstrates infrastructure-as-code for static hosting and secure CDN configuration.

<!-- ### Minecraft Server (EC2 Spot + fallback)

**Folder:** `projects/minecraft-server/`
**Idea:** A resilient Minecraft server for a small group (5 players) running on AWS EC2 Spot Instances with an on-demand fallback and an attached persistent EBS volume. Demonstrates: EC2 spot lifecycle handling, EBS persistence, automated backups, and IaC (Terraform).
**What to expect in the project folder:** architecture diagram, Terraform modules, CloudWatch alarms, and a deployment pipeline.

### Terraform VPC & Networking module

**Folder:** `projects/terraform-vpc/`
**Idea:** Reusable Terraform module for secure VPC design (public/private subnets, NAT, route tables, security groups, and optional Transit Gateway or VPC Peering). Demonstrates modular IaC, versioning, and testing (unit + integration).

### CI/CD — CodePipeline & GitHub Actions examples

**Folder:** `projects/cicd-pipelines/`
**Idea:** Example pipelines for deploying IaC and application artifacts. Includes a CodePipeline + CodeBuild example and equivalent GitHub Actions workflows showing how to build, test, and deploy infrastructure and containers.

### Container Platform — ECS / Fargate & EKS samples

**Folder:** `projects/container-platform/`
**Idea:** Two sub-projects: a lightweight ECS Fargate demo and an EKS cluster demo (infrastructure + deployment). Demonstrates networking, service discovery, secrets management, and blue/green or canary releases.

### Monitoring & Observability (CloudWatch + Grafana)

**Folder:** `projects/monitoring/`
**Idea:** Centralized logging and metrics collection for the portfolio projects. Example setup using CloudWatch (logs & metrics), embedded dashboards, and a Grafana instance (self-managed or managed) with alerts and dashboards.

### Home / Office Intranet Lab (networking + PoE)

**Folder:** `projects/home-intranet/`
**Idea:** A documented home-office intranet lab replicating the user's setup: PoE switch placement, cable routing, powerline adapter strategy, and network diagrams — useful as a non-cloud but real infra example. -->

> You can add as many projects as you like. Keep the pattern: `projects/<slug>/README.md` describing the submodule repo and linking to it.

<br/>


## 3. Standards & conventions

A central place to store conventions so all projects look and behave consistently. Example items to include in `standards/`:

* Naming conventions (resource, module, stack naming)
* Terraform / CloudFormation / CDK style guide
* Branching & release strategy
* CI job templates and secrets handling guidance
* Security checklist (IAM least privilege, encryption-at-rest/in-transit, etc.)

<br />

## 4. How to use submodules

Add a project repository as a submodule in the matching folder. Example:

```bash
# from the repository root
git submodule add git@github.com:MHooijberg/cip-minecraft-server.git projects/minecraft-server
git commit -m "Add minecraft server submodule"
```

To clone this repo including submodules:

```bash
git clone --recurse-submodules git@github.com:MHooijberg/cip_project-root.git
# OR if already cloned
git submodule update --init --recursive
```

To update a submodule (inside the submodule folder):

```bash
cd projects/minecraft-server
git pull origin main
# back to root
cd ../../
git add projects/minecraft-server
git commit -m "Update submodule pointer"
git push
```

> Tip: Keep each project in its own repo so they can have independent CI, issues, and release cycles.

<br/>


## 5. Contributing

Contributions and improvements are welcome. Please follow these steps:

1. Read `standards/` and project-specific READMEs.
2. Open an issue describing the change you want to make.
3. Fork the specific project repository you want to change (not this root repo), make your changes, and open a PR.
4. If the change requires updating the submodule pointer here, open a PR against `cip_project-root` to update the submodule reference.

<br/>


## 6. Credits & Attribution

This portfolio is released under **GPL-3.0**. You are free to share and adapt the material under the same license, provided you give appropriate credit and keep derivative works under the same license.

When using or showcasing content derived from CIP projects, please include a visible credit that links back to the original repository and the author (example):

> "Based on work from the Cloud Infrastructure Portfolio (cip_project-root) by Mark Hooijberg — [https://github.com/](https://github.com/)MHooijberg/cip_project-root (GPL-3.0)"


## 7. Todo:
- [ ] Create Lambda function README.md:
   - [ ] Add general structure to document
   - [ ] Add project structure (files & directories)
   - [ ] Add commands + Docker explanation.
- [ ] Finish Infrastructure README.md:
   - [ ] Add 'configuration and variables' section.
   - [ ] Add 'Terraform Outputs' section.
   - [ ] Add 'Trouble shooting' section.
- [ ] Setup AWS SAM
- [ ] Setup CI/CD in all repositories.
