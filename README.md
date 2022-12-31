# Installing a minimal Arch Linux in QEMU
This is a simple guide of how to install a minimal version of arch linux with your kernel configuration.
# Table of contents
1. [The-required-dependencies](#The-required-dependencies)
2. [Prepare-the-virtual-machine](#Prepare-the-virtual-machine)
3. [Kernel-configuration](#Kernel-configuration)
4. [Boot-your-virtual-machine](#Boot-your-virtual-machine)
5. [Tips](#Tips)
## The-required-dependencies.
* Install the necessary dependencies or tools to be able to make your archlinux setup.
  ```
  base-devel fakeroot bc qemu
  ```
## Prepare-the-virtual-machine
* First, create a hard disk with `qemu`, you can set your desired size.

  ```
  qemu-img create -f qcow2 yourharddisk.img 10G
  ```
* Then, download the latest Archlinux image from [here](https://archlinux.org/download/).

  NOTES: be careful to use the latest image.

* To install arch linux on the disk image, you should attach the iso file and the image file.

  ```
  qemu-system-x86_64 -enable-kvm -cdrom ARCH.iso -boot -drive file=yourharddisk.img -m 4G
  ```
  In my case, I decided to use `4G` of ram.
  
  If you want to boot with `uefi` you must install `ovmf` package and attach the `OVMF.fd` file.
  
  ```
  -bios /path/to/OVMF.fd
  ```
  It is usally at this path `/usr/share/ovmf/`.
  
* Then you can follow the [official guide](https://wiki.archlinux.org/title/installation_guide) to install arch linux properly.

## Kernel-configuration
* Go [here](https://www.kernel.org/) and download the lasted version of the linux kernel and decompress the file.

  ```
  tar -xf linux-*.*.*.tar.xz
  ```
* Create an output directory.

  ```
  mkdir kernel-build
  ```

* I decided to go with the default configuration of the kernel compilation.

  ```
  make O=../kernel-build defconfig
  ```

* Then, compile the kernel.

  ```
  make O=../kernel-build -j4 kernelimage
  ```
  At the end, you should finish with your kernel image at this path.

  ```
  kernel-build/arch/x86_64/boot/kernelimage
  ```

## Boot-your-virtual-machine
* To boot the virtual matchine, you need to specified the root partation where you install the arch linux.

  ```
  qemu-system-x86_64 -enable-kvm -hda yourharddisk.img -m 4G -kernel /path/to/kernelimage -append "root=/dev/sda* console=ttyS0 rw"
  ```
  Remember to specify the root partition.

## Tips
* To optimize the virtual machine, you should use these flags.

   ```
   -enable-kvm
   -cpu host
   -smp 4
   -vga qxl
   ```
   cpu host: To stop emulating the cpu.
   
   smp: To specify the number of threads to be used by the cpu.

   vga qxl: Is a paravirtual graphics driver with 2D support, you can use another option [here](https://wiki.archlinux.org/title/QEMU#Graphic_card).

   
   


