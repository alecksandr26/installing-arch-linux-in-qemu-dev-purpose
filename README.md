# Running Archlinux in QEMU
It's more simple than looks like, just follow the simple steps.
## The required dependencies.
* Install the necessary dependencies or tools to be able to make your archlinux setup.
  ```
  base-devel fakeroot bc qemu ovmf
  ```
## Prepare the virtual machine
* First, create a hard disk with `qemu`, you can set your desired size.

  ```
  qemu-img create -f qcow2 yourharddisk.img 10G
  ```
* Then, download the latest Archlinux image from [here](https://archlinux.org/download/).

  NOTES: be careful to use the latest image.

* To install arch linux on the disk image, you should attach the iso file and the image file.

  ```
  qemu-system-x86_64 -enable-kvm -cdrom ARCH.iso -boot -drive file=yourharddisk.img -m 4G -bios /path/to/OVMF.fd
  ```
  In my case, I decided to use `4G` of ram and to be able to boot with uefi you must attach the `OVMF.fd` file.
* Then you can follow the [official guide](https://wiki.archlinux.org/title/installation_guide) to install arch linux properly.

## Kernel configuration
* Go [here](https://www.kernel.org/) and download the lasted linux kernel.
