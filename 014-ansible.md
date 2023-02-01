### Ansible

Ansible is an open source, command-line IT automation software application written in Python. It can configure systems, deploy software, and orchestrate advanced workflows to support application deployment, system updates, and more.

Ansible’s main strengths are simplicity and ease of use. It also has a strong focus on security and reliability, featuring minimal moving parts. It uses OpenSSH for transport (with other transports and pull modes as alternatives), and uses a human-readable language that is designed for getting started quickly without a lot of training.

---

#### Architecture

Both community Ansible and Ansible Automation Platform have the concept of a control node and a managed node. The control node is where Ansible is executed from, for example where a user runs the ansible-playbook command. Managed nodes are the devices being automated, for example a Microsoft Windows server.

For automating Linux and Windows, Ansible works by connecting to managed nodes and pushing out small programs, called "Ansible modules," to them. These programs are written to be resource models of the desired state of the system. Ansible then executes these modules (over SSH by default), and removes them when finished. These modules are designed to be idempotent when possible, so that they only make changes to a system when necessary.

For automating network devices and other IT appliances where modules cannot be executed, Ansible will run on the control node. Since Ansible is agentless, it can still communicate with devices without requiring an application or service to be installed on the managed node. To increase execution capacity for devices without the ability to run modules, Ansible Automation Platform can spread automation jobs out across execution nodes using a technology called automation mesh. To understand more about how network automation is different, check out the Ansible documentation.

![](./images/image17.svg)

---

#### Inventory

Ansible inventory is a collection of hosts and their corresponding variables, used to manage and automate IT infrastructure. It serves as the source of information for Ansible, defining the hosts and groups of hosts that Ansible will manage.

An inventory file can be in simple text format, defined in a single file or multiple files in a directory. It can also be a dynamic inventory, created from a script that can pull data from cloud providers like AWS, GCE, or Azure.

The inventory file is typically organized as a series of host definitions, grouped into groups, each of which can have its own variables. Grouping hosts allows you to apply the same operations, such as running tasks, to multiple hosts at once. For example, you can define a group of web servers, another group of database servers, and another group of load balancers, each with its own set of variables.

In addition to host and group variables, the inventory file can also define "magic" variables, such as "ansible_connection", which defines the connection method to be used to communicate with the host, and "ansible_user", which defines the username to be used to log in to the host.

Example:

```bash

[db]
db.dev.ansibled

[api]
api.dev.ansibled

[webapp]
app.dev.ansibled

[environment.dev]
db.dev.ansibled
api.dev.ansibled
app.dev.ansibled

[project.ansibled:children]
environment.dev

```

---

#### Playbook

Ansible playbook is a configuration management script that defines tasks and procedures to automate the management of IT infrastructure using Ansible. It is written in YAML format and executed using the ansible-playbook command.

A playbook consists of one or more plays, each of which defines a series of tasks to be executed on one or more managed hosts. Each task is a module call, defining a specific operation to be performed, such as installing a package, copying a file, or starting a service. The tasks within a play are executed in order, from top to bottom, and can be organized into logical blocks, such as conditional execution or loops.

In addition to tasks, a play can also define variables, which can be used to customize the behavior of tasks. For example, you could define a variable that specifies the version of a package to be installed, or the location of a file to be copied. Variables can be defined at the play level, or at the playbook level, and can be overridden by more specific definitions.

Playbooks can also include "handlers", which are defined blocks of tasks that are executed based on events, such as the completion of other tasks, or the successful execution of a task. Handlers are typically used to restart services or perform other cleanup operations.

Playbooks can also include "roles", which are reusable collections of tasks, files, templates, and other configuration elements, organized into a well-defined structure. Roles can be used to encapsulate common functionality, making playbooks more modular and easier to maintain.

Example:

```bash
---
- name: Install and configure a LAMP stack
  hosts: web
  become: yes
  vars:
    apache_version: 2.4
    php_version: 7.4
  tasks:
  - name: Install Apache
    yum:
      name: httpd
      state: latest
    when: apache_version == 2.4

  - name: Start Apache service
    service:
      name: httpd
      state: started
      enabled: yes

- name: Install and configure PHP
  hosts: web
  become: yes
  vars:
    php_version: 7.4
  tasks:
  - name: Install PHP
    yum:
      name: php{{ php_version }}
      state: latest

  - name: Install PHP modules
    yum:
      name:
        - php{{ php_version }}-mysql
        - php{{ php_version }}-gd
      state: latest

  - name: Restart Apache service
    service:
      name: httpd
      state: restarted

  - name: Copy index.php file
    copy:
      src: files/index.php
      dest: /var/www/html/index.php
```

In this example, the playbook is divided into two plays:

- The first play installs Apache HTTP Server (httpd) and starts and enables the Apache service.
- The second play installs PHP and necessary modules, restarts Apache service, and copies an index.php file to the /var/www/html directory.

---

#### Plugins, Modules, and APIs

Ansible consists of three main components: plugins, modules, and APIs.

- `Plugins`: Plugins are extensions to the core Ansible functionality that allow it to perform additional tasks. There are many types of plugins, including connection plugins, inventory plugins, and lookup plugins. Connection plugins define how Ansible connects to a remote system, inventory plugins define how host and group information is obtained, and lookup plugins allow data to be retrieved from external data sources. Examples:

  - Connection plugins: The paramiko plugin is an example of a connection plugin that allows Ansible to connect to remote systems over SSH. Another example is the winrm plugin, which allows Ansible to connect to Windows systems.

  - Inventory plugins: The ini plugin is an example of an inventory plugin that allows you to define your host and group information in an INI file. Another example is the dynamic plugin, which allows you to dynamically generate your inventory from a script or database.

  - Lookup plugins: The file lookup plugin is an example of a lookup plugin that allows you to retrieve data from a file. Another example is the vault lookup plugin, which allows you to securely store sensitive data and retrieve it in your playbooks.

- `Modules`: Modules are the units of work that Ansible performs. They represent the core functionality of Ansible, such as installing packages, creating files, and managing services. Ansible includes a large collection of pre-written modules that perform a wide range of tasks, and you can also write your own custom modules if necessary. Examples:

  - Package management modules: The yum module is an example of a module that allows you to manage packages on Red Hat-based systems, while the apt module performs the same task on Debian-based systems.

  - File management modules: The file module is an example of a module that allows you to manage files on remote systems. The copy module allows you to copy files to remote systems, while the template module allows you to generate files from templates.

- `APIs`: Ansible has a REST API that allows you to interact with Ansible programmatically. You can use the API to create playbooks, execute playbooks, and manage inventory. The API provides a way to automate Ansible tasks and integrate Ansible into other systems and tools. Examples:
  - REST API: The REST API is an example of an API that allows you to interact with Ansible programmatically. You can use the API to execute playbooks, manage inventory, and perform other tasks. The API can be used to integrate Ansible into your existing workflows, automate tasks, or build custom interfaces for Ansible.

Overall, the combination of plugins, modules, and APIs gives you a powerful and flexible tool for managing your infrastructure. With plugins and modules, you can automate complex tasks with ease, and with the API, you can integrate Ansible into your existing workflows.

---
