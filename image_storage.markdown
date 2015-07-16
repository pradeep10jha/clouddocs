# Image Storage

When you create a disk image, you must choose where it is stored, under the heading `Datastore`.
You have the clice between `local_images_ssd` and `ceph`.

## Images on datastore `local_images_ssd`

When a VM is created, images on the datastore `local_images_ssd` are copied to the node where the VM will run.
This takes some copying at startup and, if the image's `persistent=yes`, copying back at shutdown, but during the run of the VM the data is local.

Always place the (small) boot disk with the OS on datastore `local_images_ssd`.
Other disks may be on datastore `ceph`, depending on your needs.

Large data images are problematic, as the disk space needs to be available on the node where the VM runs.

## Images with `persistent=yes` on datastore `ceph`

When a VM is created, images with `persistent=yes` on the datastore `ceph` are directly connected as a network disk to the node where the VM will run.
This takes no copying at startup and all data transfer will go over the network.

Large data images are possible, as no disk space is used on the node where the VM runs.

## Images with `persistent=no` on datastore `ceph`

When a VM is created, images with `persistent=no` from the datastore `ceph` are copied for the private use by the VM.
This takes some copying at startup and the copy is directly connected as a network disk to the node where the VM will run.

Large data images are possible, as no disk space is used on the node where the VM runs.