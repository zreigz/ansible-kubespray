# Single Node Kubernetes via Kubespray

Deploys a single-node Kubernetes cluster using [Kubespray](https://github.com/kubernetes-sigs/kubespray) (release-2.30).

## Prerequisites

- Python 3 + `python3-venv` on the control node
- SSH private key with access to the target node
- Target node running Ubuntu with user `ubuntu`

## Setup

```bash
git clone --recurse-submodules <this-repo>
cd ansible-kubespray
```

Edit `hosts.ini` and set the target node IP:
```ini
[k8s]
node1 ansible_host=<NODE_IP>
```

## Run

```bash
ansible-playbook main.yaml -i hosts.ini --private-key /tmp/ssh-privatekey
```

## Dry run

```bash
ansible-playbook main.yaml -i hosts.ini --private-key /tmp/ssh-privatekey --check --diff
```

## Repo structure

```
ansible-kubespray/
├── hosts.ini                        # outer inventory — set node IP here
├── main.yaml                        # main playbook
├── inventory/
│   └── group_vars/
│       ├── all/                     # kubespray global vars
│       └── k8s_cluster/            # kubernetes cluster vars
└── kubespray/                       # git submodule @ release-2.30
```

