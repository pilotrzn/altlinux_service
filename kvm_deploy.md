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
      "<host mac='52:54:00:34:c9:b4' \
       name='etcd_test' ip='192.168.122.20' />" \
       --live --config

virsh net-update default add ip-dhcp-host \
      "<host mac='52:54:00:a8:b3:78' \
       name='pgsql02' ip='192.168.122.14' />" \
       --live --config


qemu-img create -f qcow2 /home/aavdonin/hdd/qemu/qcows/alt10template 6G


virt-install --name alt10template --memory 2048 --vcpus=2 --os-variant=alt.p10 --cdrom=/home/aavdonin/hdd/iso/alt-server-10.0-x86_64.iso --network=bridge:virbr0,model=virtio --disk path=/home/aavdonin/hdd/qemu/qcows/alt10template


52:54:00:f8:0a:29

virsh net-update default add ip-dhcp-host \
      "<host mac='52:54:00:f8:0a:29' \
       name='alt10pgsql' ip='192.168.122.200' />" \
       --live --config