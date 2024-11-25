# raynix-spec
General spec for currently hypothetical improved Linux-forked kernel dubbed "Raynix"
# This is HEAVILY WIP, bear with me as things change

## A word from the repo owner

### Lack of code of conduct
Codes of conduct are often used by politically-driven saboteurs in the FOSS space to try and shatter otherwise fruitful projects. They can also be used to ensure that you reveal some important information, such as your name, which can balloon into doxxing. By lacking a code of conduct, the repo owner effectively sits as a king that can more effectively gatekeep saboteurs as long as the power doesn't get to their head. Additionally, you will be able to stay anonymous unless your job needs you to reveal yourself, for whatever reason.

### Notes on Licensing
I would have left this unlicensed, because (I am not a lawyer) it would have allowed anyone who comes across this project to use it as they see fit, so long as they don't claim the original code as not being from Raynix Team and/or the Linux Foundation. However, Linux is licensed under GPLv2, so, under license, I must do the same for Raynix. Regardless of law, I fully acknowledge the license and will act accordingly.

### Notes on compatibility-breaking changes
Raynix as it is described in this spec will fail to run a fair amount of Linux software as it currently exists, and said software will need to be tweaked in order for it to be usable, but with the kernel being a Linux fork, only some aforementioned tweaks will be needed. Drivers will also need to be reworked. This is because I'm leaning away from Linux's current design philosophy, where the kernel shoulders far too much responsibility, to the point that drivers you install have to rebuild the kernel to add the relevant code that also probably needs a binary blob. By separating responsibilities while keeping said responsibilities tightly integrated, I hope that Raynix will be more stable in general down the line.

### Is this Unix or Linux-like? Is it a distro?
Raynix as a kernel is a (currently hypothetical) fork of the Linux kernel. As a result, it is not considered a distro, and is more of a Linux-like project.

## Raynix spec

### 1. Kernel
The kernel is a fork of Linux from the Linux Foundation, built as minimally as possible for i686 and x86_64 platforms. This aims to minimize the effort needed to introduce security fixes and potential ports. Drivers and extensions to the kernel are made separately, with the "kernel bit" and supporting files built out to a folder in a new folder called /krn/add/, where the kernel would be in /krn/core.

### 2. Init
The init system is simple. In each line, the setup of the configuration file in /krn/add/set.conf is like this: `(driver folder name) (1 or 0)`. The folder name is the driver in question, and the number is boolean, and tells the init system whether or not to search the directory for, and enable, the kernel bit (aptly named "kernel.bit"). It will also take commands available from installed programs akin to currently developed init systems, so you can go from bootloader to X session, where .xinitrc will do the rest.

### 3. Programs
The recommended programs to be included with a Raynix distro are the GNU toolkit software and a minimal window manager for X11, similarly to how OpenBSD provides cwm using xenodm to get started. I, AceSoren will personally develop one in Raylib (which is where the first part of Raynix comes from) with two variants: framebuffer and OpenGL, which will automatically pass the baton if OpenGL capability is detected to improve the desktop experience.

### 4. Hardware
In the event that Raynix is ported to architectures with strange and forced screen resolutions that might not get detected (say a NeXTStation), my window manager will have the ability to make custom resolutions to better support this hardware, to be placed in an experimental tab in the resolution settings with a warning that you might not be able to see the screen if you get it wrong. Other window managers and desktop environments that are installed into a Raynix distro have the capability to detect resolutions automatically.

### 5. Filesystem
The default directory will remain mostly similar to Linux's, save for the changes to the way the kernel works. I mentioned these new folders in "1. Kernel", those being /krn, /krn/add and krn/core. /krn is the kernel folder, where Raynix itself and its addons will sit, whereas Linux often sits in /boot or /bin, varying between distributions and embedded systems. /krn/core is where Raynix will always look for the kernel, to reduce the amount of wild goose chases that can happen. Choices of filesystems will vary depending on what filesystems any chosen distro supports. If a Raynix distro only provides EXT4 and ZFS for server purposes, then other filesystems will have to be installed/compiled manually or with a package manager.

### 6. Licensing
The relations between software licenses will remain the same as with the Linux kernel because Raynix is a fork of Linux. If an Arch-based distro adopts Raynix, for example, it will live in the same legal gray area as Arch Linux itself, unless it makes changes to get away from that gray zone or go the other way. Oftentimes, licenses will be included with programs when downloaded, so I'd like to keep that trend going for legality's sake as well.

### 7. Agnosticism
Raynix should be relatively hardware-agnostic similar to Linux, regardless of the changes. If someone decides to port Raynix to a different architecture, they may have a similar amount of work to do if they did the same with Linux.
