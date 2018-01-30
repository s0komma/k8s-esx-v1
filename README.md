# k8s-esx
Kubernetes on ESX VM with Persistent Storage.

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
