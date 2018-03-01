I believe the problem is that the kernel version of the host system and the chroot environment are different. And that the chroot environment doesn’t have the right kernel information. So, after booting into the chroot’d spot instance, try the following:

uname -r to find out what the kernel of the container is, in my case 4.4.0-59
Now, we need to install the image and headers for this kernel. If you go to
ls /lib/modules
you should see that your kernel information is not actually there.
To install the kernel stuff type:
sudo apt-get install linux-image-<your kernel number>-generic
and
sudo apt-get install linux-headers-<your kernel number>-generic
relpace with your kernel number, for instance
sudo apt-get install linux-headers-4.4.0-59-generic

Then, install the nividia kernel module
sudo modprobe nivida
now try
nvidia-smi
and if it doesn’t error, and instead shows you something like