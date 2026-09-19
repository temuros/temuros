# Temur Melibaev

Infrastructure engineer. Linux, networks and production systems for 20+ years;
Kubernetes, Terraform and Ansible where the environment is closed and the
internet is not available.

Based in Tashkent, Uzbekistan. Working remotely.

## What I do

I have spent two decades being the person responsible when infrastructure
stops: Linux and Windows servers on bare metal, Cisco corporate networks,
firewalls, virtualisation, backup and recovery, offices in different cities
connected over VPN. International organisations with strict security
requirements, 50+ seat environments, no dedicated team to hide behind.

In recent years the work moved from administration to engineering. Monitoring
with Prometheus, Grafana and Alertmanager. Polkadot and Kusama validators
running around the clock, where downtime costs their owner money. My own web
products in production, from the server and the domain to deployment scripts
and incident analysis at three in the morning.

Anything repeatable goes into a script and into git. Configuring from memory
is how environments quietly drift apart.

## Current work in the open

**[quarry-fleet-lab](https://github.com/temuros/quarry-fleet-lab)** is a public
proving ground for delivering Kubernetes into a closed network, the way it
happens at an industrial site where the perimeter has no route out.

- Terraform (libvirt provider) creates the machines on KVM from code
- Kubespray installs a kubeadm cluster: Calico, containerd, persistent volumes
- The whole installation repeats with the nodes cut off from the internet;
  images arrive as files into a registry inside the perimeter
- GitOps without external dependencies: a git server and ArgoCD in the closed
  network
- Ansible roles configure clock sync, registry endpoints and storage;
  the second run reports `changed=0`
- Storage is a two-machine pair: block-level replication, a floating address
  and an arbiter that decides who may hold the volume when the link breaks
- NetworkPolicies segment the workload in both directions

The payload is a model of an open-pit mining fleet: Kafka in KRaft mode,
PostgreSQL, a stream processor in Python, three Grafana screens for three
different readers, and onboard telemetry arriving over two vehicle protocols
(EGTS and Wialon IPS) that converge into one message before anything
downstream sees them.

### Verified by breaking it

A resilience claim that has never been tested is a diagram, not a property.
Ten drills so far: a worker node killed, power cut to every node at once, a
control-plane node killed, the node holding the shift journal killed, the node
holding the registry killed, a storage machine killed, a planned storage
handover, etcd restored from a snapshot, the journal restored from a backup,
and the link between the two storage machines cut while both stayed alive.

Recovery times are recorded, and the drill logs are in the repository. Four of
those exercises found real defects, including one that every earlier drill had
missed: planned storage handover did not work at all, because killing a machine
is not the same failure as two live machines losing sight of each other.

## Stack

- **Kubernetes** kubeadm, Kubespray, k3s, Helm, Calico, containerd, registry:2, skopeo
- **Infrastructure as code** Terraform (libvirt/KVM), Ansible, cloud-init, Docker
- **Delivery** GitOps with ArgoCD, Gitea inside the perimeter, deployment scripts with sync checks
- **Observability** Prometheus, Grafana, Alertmanager, Sentry, log analysis
- **Data** Apache Kafka (KRaft), PostgreSQL, Python producers and consumers
- **Systems and networks** Debian, Ubuntu, CentOS, Windows Server, Active Directory, VMware vSphere, Cisco routing and switching, VPN, firewalls, Cloudflare

## Background

- **Network & ICT Engineer**, TEXTIMA Export Import GmbH, Tashkent, since 2018
- **Chief Computer Specialist (Key Expert)**, SOFRECO, World Bank financed
  horticulture technology programme in Uzbekistan, 2020 to 2023
- **IT System Administrator**, Goethe-Institut Tashkent, 2007 to 2018

Certified by Cisco (CCNA, CCNA Security) and Microsoft (MCP/MCSA).
Russian native, English and German at working level.

## Contact

[LinkedIn](https://www.linkedin.com/in/temur-m-52014023/) · temur.melibaev@gmail.com
