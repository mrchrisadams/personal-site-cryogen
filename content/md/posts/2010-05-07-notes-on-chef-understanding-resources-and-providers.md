

{:author "admin", :title "Notes on Chef - Understanding Resources and Providers", :date "2010-05-07 09:19:34", :publish-date "Fri, 07 May 2010 09:19:34 +0000"}



<!-- content below -->

Title: Understanding resources and providers in Chef
Date: 2010-05-07 08:36:45

Chef is a pretty huge system, and one area that I didn't quite follow before was how recipes described in cookbooks were actually executed on the client machines when they were run. One of the key ideas with chef is that when you're writing recipes, you're effectively decoupling the results you'd want from an action, from the implementation, so you end up with a cross platform way to perform a given task.

Resources and Providers
=======================

You do this primarily in chef by writing Resources, which are high level ways to describe an action, like install a software [package][], or edit a [group][] or [user][], then writing a Provider, which describes how you might actually implement this action on a given platform, or server setup.

For example on the [group] resource, when you're on a Linux system, you'll use a provider like `Chef::Provider::User::Useradd` by default, which is effectively a wrapper around a compiled binary like `useradd`, but if you're running Chef a Mac OS box, the default provider would be `Chef::Provider::User::Dscl`, which is essentially the same kind of wrapper around the `dscl` command.

It's this abstraction layer that decouples the action, from the implementation, and without understanding this, you won't get too far when writing cookbooks.

An example - the Script Resource
================================

A good example of resource and providers would be the Script resource, because it shows how the code you might write when using a resource ends up looking like a cross between bash and ruby.

<pre lang="ruby">
    script "install_something" do
      interpreter "bash"
      user "root"
      cwd "/tmp"
      code <<-EOH
      wget http://www.example.com/tarball.tar.gz
      tar -zxf tarball.tar.gz
      cd tarball
      ./configure
      make
      make install
      EOH
    end
</pre>

In the snippet above, we're doing a common task - downloading a tarfile, then doing the `configure`, `make`, `make install` dance to compile it, but in the the first few lines, we're telling the resource to use the bash provider, and to switch to the root user first, before running the command by calling actions and attributes that the Resource has made available to us. It pays to check the docs on the opscode page if you see a command that you don't recognise when looking at recipes, as they're often described in the `actions` or `attributes` section.

One trick peculiar to the Script resource, is this shortcut to run the same string of commands without needing to explicitly set the interpreter in the block:

<pre lang="ruby">
    bash "install_something" do
    user "root"
      cwd "/tmp"
      code <<-EOH
      wget http://www.example.com/tarball.tar.gz
      tar -zxf tarball.tar.gz
      cd tarball
      ./configure
      make
      make install
      EOH
    end
</pre>

As mentioned before, you have more than one Provider for a given resource. In this case, we currently have 5 different providers, that correspond to the main shells or interpreters for running scripts, listed below:

<pre lang="ruby">
    Chef::Resource::Script::Bash   bash
    Chef::Resource::Script::Csh    csh
    Chef::Resource::Script::Perl   perl
    Chef::Resource::Script::Python python
    Chef::Resource::Script::Ruby   ruby
</pre>

This post should give a some high level insight into how Resources and Providers work, but as ever, if you're working with Chef, and their wiki isn't in your bookmarks You're Doing it Wrong - check the relevant pages, and with some luck this powerful feature of chef should become a bit less cryptic.


[package]: http://wiki.opscode.com/display/chef/Resources#Resources-Package "Resources - Chef - Opscode Open Source Wiki"
[group]: http://wiki.opscode.com/display/chef/Resources#Resources-Group "Resources - Chef - Opscode Open Source Wiki"
[user]: http://wiki.opscode.com/display/chef/Resources#Resources-User "Resources - Chef - Opscode Open Source Wiki"

