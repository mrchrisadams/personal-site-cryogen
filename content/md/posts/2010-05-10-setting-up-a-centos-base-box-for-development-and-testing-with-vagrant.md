

{:author "admin", :title "Setting up a CentOS base box for development and testing with Vagrant", :date "2010-05-10 13:59:59", :publish-date "Mon, 10 May 2010 13:59:59 +0000"}



<!-- content below -->

I've been using at Vagrant at work lately to make it easier to switch between environments on projects, and to help out when testing chef recipes.

These instructions are here to help me remember how I went about building the base machines. This post will almost change in the next week or so.

If you don't know what the tool Vagrant is, these instructions won't mean much without watching this screencast demonstrating what Vagrant does, and why you might want to use it. I'd suggest taking the 15 minutes or so to watch it before reading on if you're unfamiliar with the project, as by necessity, they focus on creating a base virtual machine to begin building your own recipes on, and don't explain how to use Chef, or give much background.

They draw heavily on a gist by the excellently named Zellyn Hunter, with some instructions from the relevant page on the [opscode wiki](http://wiki.opscode.com/display/chef/Installation+on+RHEL+and+CentOS+5+with+RPMs "Installation on RHEL and CentOS 5 with RPMs - Chef - Opscode Open Source Wiki").

For simplicity, they favour using `yum` where possible for managing packages because a) it forms the basis of so many recipes when writing cookbooks in chef when you use any RedHat based flavour of Linux, and b) it should stop this guide going obsolete so quickly.

Still with us? Lets begin.

Create a bare virtual machine 
=============================

First of all, we need a virtual machine as a base. We're making a CentOS based box here, but there are also some pre-made Ubuntu based boxes available as well online linked to in the Vagrant Google Group.

In Virtual box, create a new virtual machine, giving it a descriptive name that fits the guidelines on the vagrant page. We're making a 64 bit system here, so we're need to select this in virtual box:

 Create a new VirtualBox machine
- Name: vagrant-centos64
- Operating System: Linux
- Version: Red Hat

Because we're eventually making a `.box` file that we're want others to be able to download, we need to take this into account in the resources allocated to this virtual machine, so we're going to make a dynamic hard disk that scales up to a large size, but when empty doesn't take up much space, and we'll keep the memory allocated to this machine fairly modest too. Because we have no need for graphics, or USB ports we'll leave them out of our virtual machine as well.

The specs should look something like this:

- Base Memory Size: 360 MB
- Dynamically expanding storage 40 GB
- 40 GB
- Disabled Audio
- Disabled USB

Put an OS on the virtual machine
================================

To install the OS, we need to do two things a) make sure the architecture for the install media matches that of the virtual machines and b) make sure our net install we can download the rest of the software needed to build the machine.

First we'll fetch the relevant `iso` image to mount like a virtual boot disc on our virtual machine:

    wget http://mirrors.kernel.org/centos/5.4/isos/x86_64/CentOS-5.4-x86_64-netinstall.iso

We're using a net install to begin with here, because the standard images available for us are too large to download over broadband if you share a connection in an office or and you don't have some direct fibre-optic cable or similarly zippy connection. You'll notice this image is the install image for a 64bit architecture - the process is the same is you're looking for a 32 bit based system instead, just install fetch the [32bit install iso](http://mirrors.kernel.org/centos/5.4/isos/i386/CentOS-5.4-i386-netinstall.iso "direct link to the 32 bit iso") instead.

Next we need to make we can connect to the internet and pull down the other binary files. You should have NAT (Network Address Translation) set in virtualbox, which lets your host machine act like a router.

So make sure you have ipv4 enabled, (but ipv6 switched off), and all you should need to do is have DHCP set as the way to gain a connection, and you should be able to connect to the internet to download software.

Now run when you boot the VM, choose linux-text mode, and when asked about formatting the drive, select the option to initialise the drive with a standard linux filesystem. When you're asked about and when asked about the installation process, choose the `HTTP` option, disable ipv6, and enter the following details to pull down the kernel:

- HTTP Setup:
  - Web site name: mirrors.kernel.org
  - CentOS directory: centos/5.4/os/i386

When we're given the option to select the network, we need to have a fully qualified domain name (i.e. vagrant-centos-5-4.local, not just vagrant-centos-5-4)

We'll also want to remove as much software as possible by default, so we want to customize software installation, and make sure the following is unselected when we do:

    - Dial-up networking
    - Editors
    - Text-based internet
    - Base

Now typing things into a virtual machine terminal without copy and paste gets old quickly, so lets set up port-forwarding so we can ssh into our newly created Virtualbox. The simplest way to do this is using the following invocations on the command line. We're going to make any connections to our own host machine (i.e. our laptop) on port 2222, bounce to port 22 on the guest virtual machine, and specify that this is a TCP connection.

<pre lang="ruby">
    VBoxManage setextradata <guestname> "VBoxInternal/Devices/pcnet/0/LUN#0/Config/ssh/HostPort" 2222
    VBoxManage setextradata <guestname> "VBoxInternal/Devices/pcnet/0/LUN#0/Config/ssh/GuestPort" 22
    VBoxManage setextradata <guestname> "VBoxInternal/Devices/pcnet/0/LUN#0/Config/ssh/Protocol" TCP
</pre>

Install Chef, and the Guest Additions
=====================================

Now that we have a working machine, we need to set it up to a) work with our file system so changes on our host box are reflected on it, and b) get chef on it, so we can move into config-management nirvana. First all lets add a few handy packages first though:

<pre lang="bash">
  # useful for every case
  yum install curl ftp rsync sudo time wget which

  # these are needed for building Virtualbox Additions
  yum install gcc bzip2 make kernel-devel-`uname -r`

</pre>

With the software needed, it's worth clearing off some packages that we don't need;

<pre lang="bash">
  yum erase wireless-tools gtk2 libX11 hicolor-icon-theme avahi freetype bitstream-vera-fonts
</pre>

Now that we have the prerequisites, we can now install chef, and and setup the two-way shared folders setup.

#### Shared folders

From the virtual box app, select `Devices -> Install Guest Additions...` from the menubar to make available the Virtual box disk image; we can then mount it, and depending on the architecture we're using, run the relevant guest additions script:

<pre lang="bash">
  # mount the Guest additions image thats available in dev/cdrom as a read-only disk on the mount point /mnt, using the iso9660 standard, 
  mount -o ro -t iso9660 /dev/cdrom /mnt
  sh /mnt/VBoxLinuxAdditions-amd64.run # this may be VBoxLinuxAdditions-x86.run, if you're making a 32bit VM instead
</pre>

If you're experiencing sluggish performance with shared folders, it's worth checking that you have the latest version of Virtualbox' guest editions installed. Calling the `sh /mnt/VBoxLinuxAdditions-amd64.run` command will perform a clean installation of the extensions, which can help (we're still struggling with this issue, so if you have any pointers let us know in the comments!)

##### Install chef

We'll need to add a couple of new sources before we can install chef, from the ELFF and EPEL yum repos where more recent software packages are made available:

<pre lang="bash">
  rpm -Uvh http://download.fedora.redhat.com/pub/epel/5/i386/epel-release-5-3.noarch.rpm
  rpm -Uvh http://download.elff.bravenet.com/5/i386/elff-release-5-3.noarch.rpm
</pre>

Now at this point we can now add chef. The -y means we don't have to manually okay it when it comes through. Feel free to ignore it.

<pre lang="bash">
  yum install chef -y
</pre>

##### Create the Vagrant User

The convention with vagrant is to create a group for our vagrant user, to allow any users in that group to call commands with sudo without needing passwords (as you can imagine, this makes calling remote ssh commands much simpler):

<pre lang="bash">
    groupadd admin
    useradd -G admin vagrant
    passwd vagrant
    # choose "vagrant" as the password
</pre>

##### Update visudo to for vagrant user #####

As mentioned before, we need to make a few changes to the visudo table, to allow the vagrant user to perform chef runs. In short, we need to update the PATH attribute, relax the ssh daemon's requirements before it'll accept commands sent over ssh, and create a special insecure key that grants access without needing passwords.

First of all, comment the line  saying `Defaults requiretty` in the visudo file - this option makes having an interactive teletype terminal a requirement for sudo commands to be called, so remote ssh commands that use `sudo` won't work. Switching off lets us call these commands remotely.

<pre lang="bash">
# Defaults requiretty
</pre>

Next tweak the `Defaults env_keep` entry, to add PATH, so when we switch to switch user, we still keep the same paths, like having the correct version of Ruby when calling `ohai` the tool that chef uses to check your system's setup against the desired one specified in your cookbooks:

<pre lang="ssh">

  Defaults    env_keep = "COLORS DISPLAY HOSTNAME HISTSIZE INPUTRC KDEDIR \
                          LS_COLORS MAIL PS1 PS2 QTDIR USERNAME \
                          LANG LC_ADDRESS LC_CTYPE LC_COLLATE LC_IDENTIFICATION \
                          LC_MEASUREMENT LC_MESSAGES LC_MONETARY LC_NAME LC_NUMERIC \
                          LC_PAPER LC_TELEPHONE LC_TIME LC_ALL LANGUAGE LINGUAS \
                          _XKB_CHARSET XAUTHORITY PATH" #make sure path is here
</pre>

There's more on this here on [stackoverflow](http://stackoverflow.com/questions/257616 "sudo changes PATH - why? - Stack Overflow")

</pre>

We're almost done now - we just need to supplement the PATH variable, to make admin simpler, by making commands like `ifconfig` available without needing to type the full path to them. You do this by adding this line to the `.bashrc` file for the vagrant user:

<pre lang="bash">
  export PATH=$PATH:/usr/sbin:/sbin
</pre>

Next log out, then log back in in as the vagrant user to sort out the key based access. We're going to add an insecure key that will let anyone log in to this box, so bear that in mind if you're using this on any private boxes:

<pre lang="bash">
  mkdir .ssh
  chmod 755 .ssh
  curl -L http://github.com/mitchellh/vagrant/raw/master/keys/vagrant.pub > .ssh/authorized_keys
  chmod 644 .ssh/authorized_keys
</pre>


Clean up after ourselves, and prepare for packaging the .box file
====================================================================

We'd like to keep the packaged VM size small if we can, so the next step is to clean up after ourselves somewhat with `yum` like so:

<pre lang="bash">
sudo yum clean headers packages dbcache expire-cache
</pre>

That's all the work done in the virtual machine now. Now we need to package it up with a Vagrantfile, which lists any custom adjustments, which is where we list the port forwarding instructions using the Vagrant DSL. First we create a directory, and create the Vagrantfile, somewhat like we would with a git project:

<pre lang="bash">
  mkdir centos-vagrant-64
  cd centos-vagrant-64
  vagrant init
</pre>

Next we add edit the Vagrantfile, to add the ssh port, so we can actually log into it:

<pre lang="ruby">
  Vagrant::Config.run do |config|
    # Forward the SSH port. The 'forward_port_key' should match the
    # name of the forwarded port.
    config.ssh.forwarded_port_key = "ssh"
    config.vm.forward_port("ssh", 22, 2222)
  end
</pre>

Now that we've prepared both the Virtual Machine, and the host environment, we can then package it up, to create a sharable virtual machine. If the virtual machine we created using virtualbox was called `centos-vagrant-64`, we'd pass that in like so:

<pre lang="bash">
  vagrant package --base my_base_box --include Vagrantfile
</pre>

We'll end up with a large compress file named `package.box`, which will be our virtual machine, all package up for sharing.

We can load this into our list of virtual machines available to vagrant like so, by passing in a desired name, and the path to the file. We can also to this with boxes across the internet, as long as they end with the `.box` extension, and and they're formatted to according to the guidelines in Vagrant.

<pre lang="bash">
  vagrant add vagrant-centos5.4-x64 ./package.box 
  vagrant add precompiled-vagrant-32 http://remote.server/with/pre-made-boxes/vagrant-centos5.4-i32
</pre>

Using these boxes:
==================

Now that we have these boxes available to us, a project only needs to refer to them in their Vagrantfile like so:

<pre lang="ruby">
config.vm.box = "precompiled-vagrant-32"
</pre>

And you'll be able to develop using the same environment as the other developers.

Customizing this boxes
======================

We can update vagrant boxes using this DSL, to update memory, number of virtual cpu's, or to forward more ports if need be. If we want to give this machine more resources, because it's running too slow, we can up the memory and cpu count:

<pre lang="ruby">
  config.vm.customize do |vm|
    vm.memory_size = 2048
    vm.cpu_count = 2
  end
</pre>

If we we're working with the web, we'll want to add another forwarded port, but _remember to update the firewall rules too_:

<pre lang="ruby">
  Vagrant::Config.run do |config|
    # Forward apache
    config.vm.forward_port("web", 80, 8080)
  end
</pre>

Now what?
=========

This should give a decent grounding on how to prepare virtual machines for sharing with others, but be sure to check the [extensive documentation on the Vagrant website](http://vagrantup.com/docs/getting-started/index.html "Vagrant - Getting Started").

If you're interested in giving Vagrant a spin, and you're using CentOS, you might want to try building a system using these boxes


