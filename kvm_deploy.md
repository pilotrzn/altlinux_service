предварительно созданы копии образов

virt-install --name alt9-k8s-worker01 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-worker01.qcow2,bus=virtio --import \
--network bridge:br0 \
--os-variant=alt.p9 &

virt-install --name alt9-k8s-ctrl --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-ctrl.qcow2,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-install --name alt9-k8s-worker02 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-worker02.qcow2,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-viewer --connect qemu:///system --wait alt9-k8s-worker01

virt-install --name etcd01 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/DATA/qemu/etcd01,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-install --name alt9-k8s-worker01 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/DATA/qemu/alt-p9-k8s-worker01.qcow2,bus=e1000e --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

/home/aavdonin/DATA/qemu


virt-clone -o etcd01 -n etcd02 -f /home/aavdonin/DATA/qemu/etcd02 --connect=qemu:///system



virsh net-update default add ip-dhcp-host \
      "<host mac='52:54:00:28:1f:7b' \
       name='etcd02' ip='192.168.122.11' />" \
       --live --config

virsh net-update default add ip-dhcp-host \
      "<host mac='52:54:00:28:1f:8b' \
       name='etcd03' ip='192.168.122.12' />" \
       --live --config