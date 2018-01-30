# Kubernetes on the VMWare ESX
This tutorial will walk you through setting up Kubernetes on VMWare ESX VM's with persistant storage. 

# Target Audience
The target audience for this tutorial is someone planning to create a Kubernetes cluster on VMWare ESX platform as this helps to support existing VM infra with container platform. .

# Cluster Details
- Kubernetes 1.9.2
- Docker 1.12.6
- CNI Based Networking
- CSI Based Storage

# Platform:
VMWare ESXi on 3 servers and VM's created one on each.
Datastore for persistant storage across servers

1. Install VMWare_bootbank_esx-vmdkops-service_0.20.15f5e1d-0.0.1.vib on all the ESXi Servers.
    - esxcli software vib install -v /tmp/VMWare_bootbank_esx-vmdkops-service_0.20.15f5e1d-0.0.1.vib --no-sig-check
2. Create VM's for the Kuberentes cluster and form cluster
3. copy csi-vsphere binary to /usr/bin on all the VM's
4. Create csi-vsphere-node.service service on all the K8s worker nodes
    - mkdir -p /var/lib/kubelet/plugins/com.thecodeteam.vsphere/disks
    - systemctl enable csi-vsphere-node.service
    - systemctl start csi-vsphere-node.service 
5. Master Node-
     kubectl apply -f csi-vsphere-controller.yaml
6. Test redis container with PV
   - Apply pvc.yaml
   - Apply redis.yaml
   - Kill the redis as it reloated to another node with same volume

Cleaning Up
