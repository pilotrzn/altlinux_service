предварительно созданы копии образов

virt-install --name alt9-k8s-worker01 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-worker01.qcow2,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-install --name alt9-k8s-ctrl --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-ctrl,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-install --name alt9-k8s-worker02 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-worker02.qcow2,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-viewer --connect qemu:///system --wait alt9-k8s-worker01 &


virt-install --name alt9-srv01 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-srv01.qcow2,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-clone -o alt9-srv01 -n alt9-srv03 -f /home/aavdonin/hdd/qemu/alt9-srv03.qcow2 --connect=qemu:///system



# virsh net-update default add-last ip-dhcp-host \
      '<host mac="52:54:00:9a:96:e5" name="etcd01" ip="192.168.122.100"/>' \
      --live --config --parent-index 0

virsh net-update default add-last ip-dhcp-host \
      '<host mac="52:54:00:9a:96:e5" name="etcd01" ip="192.168.122.100"/>' \
      --live --config --parent-index 0

virsh net-update default add-last ip-dhcp-host \
      '<host mac="52:54:00:9a:96:e6" name="etcd02" ip="192.168.122.101"/>' \
      --live --config --parent-index 0

virsh net-update default add-last ip-dhcp-host \
      '<host mac="52:54:00:9a:96:e7" name="etcd03" ip="192.168.122.102"/>' \
      --live --config --parent-index 0



virsh net-update

# virsh net-update default add-last ip-dhcp-host \
      '<host id="00:01:00:01:1a:ff:2b:ff:52:54:00:8a:11:4c" ip="2001:db8::1222"/>' \
      --live --config --parent-index 1



52:54:00:9a:96:e2

virt-install --name alt9-etcd01 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-etcd01,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &


alt.p10



<network>
  <name>default</name>
  <uuid>9b20888b-c03e-44ec-aa07-5d883701e37f</uuid>
  <forward mode='nat'/>
  <bridge name='virbr0' stp='on' delay='0'/>
  <mac address='52:54:00:55:72:61'/>
  <ip address='192.168.122.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.122.2' end='192.168.122.254'/>
      <host mac='52:54:00:9a:96:e2' name='alt9-k8s-ctrl' ip='192.168.122.2'/>
      <host mac='52:54:00:9a:96:e3' name='alt9-k8s-worker01' ip='192.168.122.3'/>
<!--       <host mac='52:54:00:9d:41:08' name='alt9-srv01' ip='192.168.122.4'/>
      <host mac='52:54:00:85:c9:b3' name='alt9-k8s-worker01' ip='192.168.122.11'/> -->
    </dhcp>
  </ip>
</network>



virsh dumpxml vm > new_vm_name.xml






ff:56:50:4d:98:00:02:00:00:ab:11:6a:b0:98:a9:68:3f:f4:e2
ff:56:50:4d:98:00:02:00:00:ab:11:6a:b0:98:a9:68:3f:f4:e3
00:00:ab:11:f9:2a:c2:77:29:f9:5c:00