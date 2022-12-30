# Running Archlinux in QEMU
It's more simple than looks like, just follow the simple steps.
## The required dependencies.
* Install the necessary dependencies or tools to be able to make your archlinux setup.
  ```
  base-devel fakeroot bc qemu
  ```
## Prepare the virtual machine
* First, create a hard disk with `qemu`, you can set your desired size.
  ```
  qemu-img create -f qcow2 yourharddisk.img 10G
  ```
* Then, download the latest Archlinux image from [here](https://archlinux.org/download/).

