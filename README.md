## Vagrant-getting-Started Tutorial

One tool for creating full development environments is Vagrant. Vagrant reduces the time required to build up development environments, improves development/production parity, and eliminates the need for the "it works on my machine" justification. All of these benefits come from an intuitive process and emphasis on automation.

Follow the link below to install vagrant:
https://developer.hashicorp.com/vagrant/install

The first step to configure any Vagrant project is to create a Vagrantfile. The Vagrantfile allows you to:

* Make sure to mark the project's root directory. Vagrant's configuration settings are mostly based on this root directory.
* Specify the type of machine and software you'll need to complete your project, the software you want to install, and how you want to access it.

### Initialize the project
* The built-in Vagrant command `**vagrant init**` is used for initializing a project and this command can take a box name and URL as arguments. With this command, Vagrant installed the specified box when the project is initialized.

```vagrant init <box name or URL>```

for example, the hashicorp/bionic64 box:

```vagrant init hashicorp/bionic64```

Vagrant uses a base image (Known as "box") to quickly clone a virtual machine, saving time and effort compared to developing a virtual machine from scratch. Upon creating a new Vagrantfile, the first thing to do is to choose which of these base images—referred to as "boxes" in Vagrant—to use for your Vagrant environment.

Sometimes you may want to install a box without creating a new Vagrantfile. For this you would use the `box add` subcommand.