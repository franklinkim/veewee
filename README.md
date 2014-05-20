# Building a Vagrant BaseBox for VirtualBox with Veewee

> Quick walkthrough how to build a BaseBox for Vagrant with Veewee.

## Requirements

* VirtualBox
* Vagrant
* Bundle

### VirtualBox

Download and install the latest [VirtualBox release][virtualbox]

### Vagrant

Download and install the latest [Vagrant release][vagrant]

### Bundle

```
$ gem install bundle
```

## Building a BaseBox

```
$ git clone https://github.com/franklinkim/veewee.git
$ cd veewee
```

Run `bundle` to install dependencies run:

```
$ bundle install
```

Check and edit the `Gemfile` for newer versions:

```
$ bundle outdated
```

Define your vm with a template:

```
$ bundle exec veewee vbox define 'ubuntu-12.04.3' 'ubuntu-12.04.3-server-amd64'
```

Edit the definition files to customize the base box:

```
...
├── definitions
│   └── ubuntu-12.04.3
│       ├── base.sh
│       ├── cleanup.sh
│       ├── definition.rb
│       ├── preseed.cfg
│       ├── vagrant.sh
│       ├── virtualbox.sh
│       ├── vmtools.sh
│       └── zerodisk.sh
...
```

Build, validate and export the base box:

```
# build, get some coffee
$ bundle exec veewee vbox build 'ubuntu-12.04.3' --workdir=/Users/franklin/Workspaces/veewee/veewee-ubuntu-12.04.3

# export, ignore errors that you can
$ bundle exec veewee vbox validate 'ubuntu-12.04.3'

# export
$ vagrant package --base 'ubuntu-12.04.3'
```

## Adding the BaseBox

Add the newly created box to vagrant with:

```
$ vagrant box add 'ubuntu-12.04.3' 'ubuntu-12.04.3.box'
```

## Cleanup

When finished you can destroy the box with:

```
$ bundle exec veewee vbox destroy 'ubuntu-12.04.3'
```

## References: 

* [spilth.org][splith.org]
* [maxheapsize.com][maxheapsize.com]
                    
[vagrant]: http://www.vagrantup.com/downloads.html
[virtualbox]: https://www.virtualbox.org/wiki/Downloads
[splith.org]: http://spilth.org/blog/2013/01/21/automated-vm-generation-with-veewee-jenkins-and-amazon-s3/
[maxheapsize.com]: http://maxheapsize.com/2013/05/26/getting-started-with-veewee-and-vagrant/
