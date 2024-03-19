## Vagrant-getting-Started Tutorial

One tool for creating full development environments is Vagrant. Vagrant reduces the time required to build up development environments, improves development/production parity, and eliminates the need for the "it works on my machine" justification. All of these benefits come from an intuitive process and emphasis on automation.

Follow the link below to install vagrant:
(https://developer.hashicorp.com/vagrant/install)

The first step to configure any Vagrant project is to create a Vagrantfile. The Vagrantfile allows you to:

* Make sure to mark the project's root directory. Vagrant's configuration settings are mostly based on this root directory.
* Specify the type of machine and software you'll need to complete your project, the software you want to install, and how you want to access it.

### Initialize the project

you can added a box to Vagrant either by initializing or adding it explicitly.
* The built-in Vagrant command `vagrant init` is used for initializing a project and this command can take a box name and URL as arguments. With this command, Vagrant installed the specified box when the project is initialized.

```
vagrant init <box name or URL>
```

for example, for the hashicorp/bionic64 box:

```
vagrant init hashicorp/bionic64
```

Vagrant uses a base image (Known as `box`) to quickly clone a virtual machine, saving time and effort compared to developing a virtual machine from scratch. Upon creating a new Vagrantfile, the first thing to do is to choose which of these base images—referred to as "boxes" in Vagrant—to use for your/the Vagrant environment.

Sometimes you may want to install a box without creating a new Vagrantfile. For this you would use the `box add` subcommand.
You can add a box to Vagrant with `vagrant box add`. This stores the box under a specific name so that multiple Vagrant environments can re-use it. for example;
```
vagrant box add hashicorp/bionic64
```
to add `hashicorp/bionic64` box to vagrant. This will download the box named hashicorp/bionic64 from HashiCorp's Vagrant Cloud box catalog. Boxes are broken down into two parts—*the username `hashicorp` and the box name `bionic64`*—separated by a slash. you can also specify boxes via URLs or local file paths.

### Use a box
after adding a box to Vagrant either by initializing or adding it explicitly, the project is then configure to use it as base image. Open the Vagrantfile in the project directory and enter the code
```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
end
```
`PS: If the box was not added before, Vagrant will automatically download and add the box when it is run.`

You may specify an explicit version of a box by specifying config.vm.box_version for example:
```
config.vm.box_version = "1.0.282"
```
You may also specify the URL to a box directly using config.vm.box_url:
```
config.vm.box_url = "https://vagrantcloud.com/hashicorp/bionic64"
```
## Boot an environment --> Bring up a virtual machine
After  initializing the vagrant project and configured a box for it to use, it is time to boot up the Vagrant environment. sping up a virtual machine with:
```
varant up
```
In abount a minute or two , this command will finish and you will have a virtual machine running Ubuntu.

vagrant will do it thing and You will not actually see anything though, since Vagrant runs the virtual machine without a UI. after the successful running of the virtaul machine, you can SSH into the machine:
```
vagrant ssh
```
This command will drop you into a full-fledged SSH session. where you can interact with the machine.

when done with the Virtual machine, stop the machine that Vagrant is managing and remove all the resources created during the machine-creation process with the following command: and follow the prompt
```
vagrant destroy
```

**PS:** The vagrant destroy command does not remove the downloaded box file. To list the existing boxes, use
```
vagrant box list
```
Remove the box file with the `remove` subcommand, providing the `name of your box`. e.g
```
vagrant box remove hashicorp/bionic64
```

### Synchronize local and guest files
Vagrant shares your project directory—which houses the Vagrantfile—by default with the /vagrant directory on your guest computer.

Files are automatically synchronised between the guest computer and Vagrant. In this manner, you can run files in your virtual development environment and edit them locally.
```
Tip

When you vagrant ssh into your machine, you're in /home/vagrant, which is a different directory from the synced /vagrant directory.
```
* To see and edit the content in the synced directory, always reference `/vagrant`. for example, to list the contents in the synce directory use;
```
ls /vagrant
```
for list content in the VM directory just use `ls`

With synced folders, You can keep using your own editor on your host machine and have the files sync into the guest machine

### Share an environment
Vagrant makes it easy to share and collaborate on development environments (VM). The primary feature to do this in Vagrant is called `Vagrant Share`.

*Vagrant Share is a plugin that lets you share your Vagrant environment to anyone around the world with an Internet connection. It will give you a URL that will route directly to your Vagrant environment from any device in the world that is connected to the Internet.*

Vagrant share requires ngrok. If you don't have ngrok, follow their [install documentation](https://ngrok.com/download) to install it.

```
Warning

**The Vagrant Share service is not designed to serve production-level traffic. Only share development or Q/A environments, not production content.**
```
### Install the plugin
Install vagrant share.
```
vagrant plugin install vagrant-share
```

### Share the environment
Next, run vagrant share:
```
vagrant share
```

## Rebuild and Teardown an environment
You may pick up where you left off with your project when you're ready to revisit it at anytime.
* To start a box, run `vagrant up.`
* Suspending the virtual machine will stop it and save its current running state. Suspend the machine with `vagrant suspend`

Suspending your machine is intended for stopping and starting work quickly. The downside is that the virtual machine will still use disk space while suspended, and requires additional disk space to store the state of the virtual machine RAM.
* Halting the virtual machine will gracefully shut down the guest operating system and power down the guest machine. Halt your machine with `vagrant halt`

Halting your machine will cleanly shut it down, preserving the contents of disk and allowing you to cleanly start it again. Restart your machine.
A halted guest machine will take more time to start from a cold boot and will still consume disk space.
* Destroying the virtual machine will remove all traces of the guest machine from your system. It'll stop the guest machine, power it down, and reclaim its disk space and RAM. Destroy the machine with `vagrant destroy`

It takes even longer to bring a machine up once you destroy it, and the machine's state will not be saved.

**Again, when you are ready to work again, just issue a vagrant up.**