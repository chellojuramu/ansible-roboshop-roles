# RoboShop Ansible Roles: Role-Based Enterprise Architecture 🤖

This repository contains the professional-grade **Ansible Roles** configuration for the **RoboShop** microservices stack. The project has been refactored from standalone playbooks into a modular, industry-standard directory structure to ensure high reusability and maintainability.

## 🏗️ Repository Structure

Following the **DRY (Don't Repeat Yourself)** principle, the automation is organized into specialized components:

* **`roles/`**: Contains independent, reusable automation logic for each service (MongoDB, Redis, MySQL, RabbitMQ, Catalogue, etc.).
* **`group_vars/`**: Centralized location for global variables, separating configuration from automation logic.
* **`roboshop.yaml`**: The master orchestration playbook that calls the necessary roles in the correct dependency order.
* **`ansible.cfg`**: Project-level configuration to manage role paths and default settings.
* **`inventory.ini`**: Environment-specific host definitions.



## 🎯 Modular Automation Strategy

This project implements advanced Ansible features to manage a complex 3-tier application:

* **Common Role Integration**: Universal system tasks like `app_setup` and `nodejs_setup` are extracted into a `common` role to be shared across all microservices.
* **Role Dependencies**: Specific services leverage the `meta` directory to automatically trigger prerequisite roles (e.g., ensuring `common` is ready before `catalogue` starts).
* **Dynamic Templating**: Uses Jinja2 templates (`.j2`) to inject environment variables into systemd unit files at runtime.
* **Confidentiality Management**: Built to separate non-confidential data (URLs) from confidential data (passwords).



## 🛠️ Technology Stack

* **Orchestration**: Ansible
* **Infrastructure**: AWS (EC2, Route53, Security Groups)
* **OS Standards**: RHEL 9 / CentOS (Enterprise Standard)
* **Languages**: NodeJS, Java (Maven), Python
* **Datastores**: MySQL, MongoDB, Redis, RabbitMQ

## 📂 Role Map

| Role | Responsibility |
| :--- | :--- |
| **`common`** | Shared application and system-level setup logic. |
| **`mongodb`** | NoSQL database configuration and schema loading. |
| **`mysql`** | Relational database setup with idempotent security checks. |
| **`redis`** | In-memory cache configuration for session management. |
| **`rabbitmq`** | Message broker setup for asynchronous processing. |
| **`catalogue`** | NodeJS-based microservice for product management. |
| **`user`** | NodeJS-based authentication and profile service. |
| **`shipping`** | Java-based service built with Maven. |

## 🚀 Execution & Usage

### 1. Provision Infrastructure
Deploy the AWS resources:
```bash
ansible-playbook 01-create-infrastructure.yaml
