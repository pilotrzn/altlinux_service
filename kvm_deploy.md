предварительно созданы копии образов

virt-install --name alt9-k8s-worker01 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-worker01.qcow2,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-install --name alt9-k8s-ctrl --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-ctrl.qcow2,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

virt-install --name alt9-k8s-worker02 --memory 2048 --vcpus 2 \
--disk /home/aavdonin/hdd/qemu/alt9-k8s-worker02.qcow2,bus=virtio --import \
--network bridge:virbr0 \
--os-variant=alt.p9 &

