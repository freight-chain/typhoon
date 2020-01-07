# <img src="header.png" alt="Freight Trust Typhoon" height="60px">

> Freight Trust Typhoon HA-Cluster


```bash
module "freightlayer" {
  source = "git::https://github.com/freight-chain/typhoon/google-cloud/kubernetes?ref=v1.17.0"

  # Google Cloud
  cluster_name  = "freightlayer"
  region        = "us-central1"
  dns_zone      = "freightlayer.net"
  dns_zone_name = "freightlayer-zone"

  # configuration
  ssh_authorized_key = "ssh-rsa AAAAB3Nz..."

  # optional
  worker_count = 2
}

# Obtain cluster kubeconfig
resource "local_file" "kubeconfig-freightlayer" {
  content  = module.freightlayer.kubeconfig-admin
  filename = "/home/user/.kube/configs/freightlayer-config"
}
```

```bash
$ terraform plan
Plan: 62 to add, 0 to change, 0 to destroy.
$ terraform apply
Apply complete! Resources: 62 added, 0 changed, 0 destroyed.
```

```bash
$ export KUBECONFIG=/home/user/.kube/configs/freightlayer-config
$ kubectl get nodes
NAME                                       ROLES    STATUS  AGE  VERSION
freightlayer-controller-0.c.freightlayer-net.internal  <none>   Ready   6m   v1.17.0
freightlayer-worker-jrbf.c.freightlayer-net.internal   <none>   Ready   5m   v1.17.0
freightlayer-worker-mzdm.c.freightlayer-net.internal   <none>   Ready   5m   v1.17.0
```

---
(c) 2020 - FreightTrust & Clearing Corporation . All Rights Reserved of their respective owners.