## Modifying the System Bootloader

If you are on a physical machine you can press any key during boot to interrupt
the boot process and choose which kernel you want to use, but **you can also do
it from the command line when you're already logged in**.

Side note: `dracut` is a command for initramfs files for booting the kernel.
When you install/update the kernel it usually creates these automatically (they
can be found in `/boot` -- those "vmlinuz" files). If not, use `dracut`.

`grub2-set-default 0` tells GRUB to boot the _newest_ version of the kernel.
`grub2-set-default 1` tells GRUB to boot the _2nd newest_ version of the kernel.
`grub2-set-default 2` tells GRUB to boot the _3rd newest_ version of the kernel.

Note: if you don't have more than 1 other kernel available an you set-default to
2 (out of range), it will just boot the newest one. `grub2-set-default` won't
throw an error.
