# santi-homelab
Self-hosted infrastructure project — Linux, Docker, Ansible, networking. Where I keep practicing what I learned at college.

mkdir -p docs ansible/playbooks ansible/roles ansible/inventory \
         docker scripts network terraform .github/workflows assets

touch docs/architecture.md docs/services.md docs/lessons-learned.md \
      ansible/inventory/hosts.yml ansible/ansible.cfg \
      docker/docker-compose.yml \
      scripts/backup.sh scripts/health-check.sh \
      network/vlan-config.md network/firewall-rules.md \
      .gitignore .editorconfig CONTRIBUTING.md
