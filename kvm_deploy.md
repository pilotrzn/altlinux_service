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
--disk /home/aavdonin/DATA/qemu/etcd01,bus=scsi --import \
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


qemu-img create -f qcow2 /home/aavdonin/qemu/qcows/altserver101 6G


virt-install --name altserver101 --memory 2048 --vcpus=2 --os-variant=alt.p10 --cdrom=/home/aavdonin/qemu/iso/alt-server-10.1-x86_64.iso --network=bridge:virbr0,model=virtio --disk path=/home/aavdonin/qemu/qcows/altserver101

virt-install --name alt10cik --memory 2048 --vcpus 2 \
--disk /home/aavdonin/qemu/qcows/alt-p10-cloud-v9-x86_64.qcow2,bus=scsi --import \
--controller type=scsi,model=virtio-scsi \
--network bridge:virbr0 --os-variant=alt.p10 &


52:54:00:f8:0a:29

virsh net-update default add ip-dhcp-host \
      "<host mac='52:54:00:62:99:c6' \
       name='pgrsv01' ip='192.168.122.80' />" \
       --live --config

virsh net-update default add ip-dhcp-host \
      "<host mac='52:54:00:1c:ec:d3' \
       name='pgrsv02' ip='192.168.122.81' />" \
       --live --config

virsh net-update default add ip-dhcp-host \
      "<host mac='52:54:00:b6:97:90' \
       name='pgmon' ip='192.168.122.82' />" \
       --live --config



qemu-img create -f qcow2 /home/aavdonin/qemu/templates/orlinux9 10G

virt-install --name orlintemplate \
--memory 2048 \
--vcpus 2 \
--cdrom=/home/aavdonin/qemu/iso/OracleLinux-R9-U2-x86_64-dvd.iso \
--disk /home/aavdonin/qemu/templates/orlinux9 \
--network bridge:virbr0 \
--os-variant=ol8.5 &

virt-install --name ubuntu --memory 4096 --vcpus 4 \
--disk /home/aavdonin/qemu/qcows/ubuntu-srv,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=ubuntu20.04 &


virt-clone -o ubuntutemplate -n pgrsv01 -f /home/aavdonin/qemu/disk01/pgrsv01

virt-clone -o ubuntutemplate -n pgrsv02 -f /home/aavdonin/qemu/disk02/pgrsv02

virt-clone -o ubuntutemplate -n pgmon -f /home/aavdonin/qemu/disk03/pgmon

52:54:00:62:99:c6


qemu-img resize path_to_img +xG
growpart /dev/vda 2
xfs_growfs /dev/vda2

virt-sysprep --operations defaults,-ssh-userdir,customize -d vmname 

qemu-img create -f qcow2 /home/aavdonin/qemu/templates/ubuntutemplate 4G

virt-install --name ubuntutemplate --memory 4096 --vcpus 4 \
--cdrom=/home/aavdonin/qemu/iso/ubuntu-20.04.5-live-server-amd64.iso \
--disk /home/aavdonin/qemu/templates/ubuntutemplate \
--network bridge:virbr0 --os-variant=ubuntu20.04 &