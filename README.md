# IPU Automation Suite

This repository automates the provisioning, deployment, and image management for Intel IPU-based lab infrastructures across multiple nodes. It offers scripted and Ansible-based workflows for multi-hop, chained SSH environments often found in labs.

## What does this do?

- Automatically copies, extracts, and updates system images (such as `saiserver` and `imc-config`) for IPU hosts, Link Partners, Management Consoles, and Compute nodes.
- Enables secure file transfers and remote update tasks, even in networks where each node is only accessible from the previous node in the chain.
- Facilitates reliable firmware and image deployment matching the required network topology for IPU testbeds and clusters.


## Features

- **Automated System Image Management:** Copy, extract, and deploy updates with minimal manual intervention.
- **Multi-Hop SSH Automation:** Handles chained connections and execution, ensuring updates reach otherwise inaccessible hosts.
- **Consistency and Repeatability:** Ensures reliable updates and reproducible results for lab and production IPU deployments.


## Topology

- The user is expected to run these scripts on a local machine and direct access to the Host and Link Partner (LP).
- The automation scripts in this repository use the LP for installation and image management.
- The Link Partner is connected to IMC via 100.0.0.x network (100.0.0.1 on LP and 100.0.0.100 on IMC).

```text

                            +----------------------+
                            | User @ control-node  |
                            +----------------------+
                                        |
                                        |
                        --------------------------------------------+
                        |                                           |
                        |                                           |
                +---------------------------+                       |
                |           HOST            |                       |
                |                           |                       |
                |   +==IPU==============+   |               +---------------+
                |   |        |          |   |               |               |
                |   |  ACC <==ssh= IMC <===========ssh============ LP       |
                |   |        |          |   |               |               |
                |   +===================+   |               +---------------+
                |                           |
                +---------------------------+

```

## Requirements

- Bash and SSH access on all target nodes.
- Ansible (for playbooks) with passwordless SSH setup where needed.
- Availability of all required system images.

## Getting Started

1. Clone this repository on your local machine (control node).
2. Update `group_vars`, `inventory` and connection details for your specific topology.
3. Run the provided scripts or Ansible playbooks to push updates as needed.
```bash
ansible-playbook playbooks/ipu_setup.yml
```

## License

Proprietary — use restricted to internal IPU lab environments.
