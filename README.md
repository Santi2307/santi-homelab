<div align="center">

# santi-homelab

**A self-hosted infrastructure project where I practice what I learned at Seneca — Linux, Docker, Ansible, networking.**

Built and broken on purpose so I can learn how to fix it.

[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![Linux](https://img.shields.io/badge/Linux-RHEL%20%7C%20Ubuntu-orange.svg)]()
[![Ansible](https://img.shields.io/badge/Ansible-2.16+-red.svg)]()
[![Docker](https://img.shields.io/badge/Docker-blue.svg)]()
[![License](https://img.shields.io/badge/License-MIT-green.svg)]()

</div>

---

## What's this?

After graduating from Seneca's Computer Systems Technology program, I wanted to keep practicing the skills I picked up across courses like **OPS445** (Linux scripting), **APL701** (Ansible automation), **SEC220** (security hardening), and **CSN305** (networking). Instead of just running through course labs again, I built infrastructure I actually use every day at home.

This repo is the complete, documented version of that work — playbooks, configs, network diagrams, and the lessons I learned along the way.

## Services running here

| Service       | Purpose                            | Stack                    | Status |
|---------------|------------------------------------|--------------------------|--------|
| Pi-hole       | Network-wide ad blocking via DNS   | Docker, DNS              | Planned |
| Nextcloud     | Personal cloud storage             | Docker, PostgreSQL       | Planned |
| Jellyfin      | Self-hosted media server           | Docker                   | Planned |
| Prometheus    | Metrics collection                 | Docker                   | Planned |
| Grafana       | Dashboards and alerting            | Docker                   | Planned |
| Wireguard     | VPN for remote access              | Linux, Ansible           | Planned |

## Architecture

```
                     [ Internet ]
                          |
                  +-------+-------+
                  |   Router      |   (pfSense - VLAN aware)
                  +-------+-------+
                          |
        +-----------------+-----------------+
        |                 |                 |
   [ VLAN 10 ]       [ VLAN 20 ]       [ VLAN 30 ]
   Work / Servers    IoT devices       Guest WiFi
        |
        v
   +------------------------------+
   |   Ubuntu Server VMs          |
   |   - docker-host  (Pi-hole,   |
   |                 Nextcloud)   |
   |   - media-host  (Jellyfin)   |
   |   - monitoring   (Prometheus |
   |                  + Grafana)  |
   +------------------------------+
```

See [`docs/architecture.md`](docs/architecture.md) for the full breakdown.

## Project structure

```
santi-homelab/
├── ansible/              Ansible playbooks, roles, and inventory
│   ├── playbooks/        Top-level playbooks (initial-setup.yml, etc.)
│   ├── roles/            Reusable Ansible roles
│   └── inventory/        Host definitions per environment
├── docker/               Docker Compose stacks for each service
├── network/              Network configuration docs (VLANs, firewall)
├── scripts/              Helper scripts (backups, health checks)
├── terraform/            (Future) IaC for cloud workloads
├── docs/                 Architecture, services, lessons learned
└── .github/workflows/    CI for linting playbooks
```

## Quick start

```bash
# Clone the repo
git clone https://github.com/Santi2307/santi-homelab.git
cd santi-homelab

# Install Ansible dependencies
ansible-galaxy install -r ansible/requirements.yml

# Test connectivity to all hosts
ansible -i ansible/inventory/hosts.yml all -m ping

# Run the initial setup playbook on a fresh server
ansible-playbook -i ansible/inventory/hosts.yml ansible/playbooks/initial-setup.yml
```

## What I've learned so far

Documented in [`docs/lessons-learned.md`](docs/lessons-learned.md). Highlights:

- **SELinux is unforgiving** — half my early issues were SELinux contexts I didn't understand
- **Idempotency matters** — running a playbook twice should never break anything
- **DNS is always the problem** — Pi-hole taught me more about DNS than CSN305 did
- **Backups need to be tested** — an untested backup is just hope

## Skills demonstrated

- **Linux administration:** RHEL/Ubuntu, systemd, LVM, SELinux, networking
- **Automation:** Ansible playbooks, roles, idempotent design
- **Containers:** Docker, docker-compose, rootless Podman
- **Networking:** VLANs, firewall rules, DNS, VPN, OSPF basics
- **Monitoring:** Prometheus, Grafana, alerting
- **Security:** SSH hardening, firewalld, fail2ban, secrets management

## Roadmap

- [x] Initial repo structure
- [ ] Day 1 — Set up first Ubuntu Server VM with UTM
- [ ] Ansible role: hardened-base (SSH, firewall, fail2ban)
- [ ] Docker stack: Pi-hole on the docker-host VM
- [ ] Wireguard VPN for remote management
- [ ] Prometheus + Grafana dashboards
- [ ] Nextcloud with PostgreSQL
- [ ] Migrate from VMs to a Raspberry Pi cluster (eventually)

## About me

I'm Santiago — IT & Systems Specialist based in Toronto, Canada. I built this homelab to keep growing after graduation. If you're hiring or just want to talk infrastructure, [reach out](https://santi-portafolio.vercel.app).

[Portfolio](https://santi-portafolio.vercel.app) · [LinkedIn](https://linkedin.com/in/santiagodelgado23) · [Email](mailto:santiagodelgadosanchez9@gmail.com)

---

<div align="center">

**License:** MIT · Built in Toronto

</div>
