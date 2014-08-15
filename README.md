openclerk-chef
==============

Chef cookbooks and configuration for installing [Openclerk](http://openclerk.org).

## Getting started

Follow the instructions from the excellent 
[Getting Started with Chef](http://gettingstartedwithchef.com/first-steps-with-chef.html) tutorial, on a brand new server as `root`:

1. Install system prerequisites:

```
apt-get install git ruby1.9.1 ruby1.9.1-dev make
```

1. Install `chef-solo`

```
curl -L https://www.opscode.com/chef/install.sh | bash
```

1. Install [librarian-chef](https://github.com/applicationsonline/librarian-chef)

```
gem install librarian-chef
```

1. Extract this repository into `/root/chef-repo`: 

```
git clone https://github.com/soundasleep/openclerk-chef.git /root/chef-repo
```

1. Configure `/root/chef-repo/web.json` based on the provided `web.json` - setting the passwords in `mysql` is particularly important.
1. Install the [openclerk cookbook](https://github.com/soundasleep/openclerk-cookbook) and dependencies through librarian-chef

```
cd /root/chef-repo
librarian-chef install      # (or `librarian-chef update` to pick up updated cookbooks)
```

1. Execute chef to install Openclerk and its software dependencies: 

```
chef-solo -c solo.rb -j web.json
```

1. Visit http://localhost/ and everything should be running! If not, check `/var/log/apache2/error.log` for any errors.

## Uses `librarian-chef`

After extracting lots of cookbooks manually with `knife`, I got fed up of typing the same commands over 
and over - so this chef repository uses `librarian-chef` for automating recipe dependencies and versions.
This lets us define cookbooks using a DSL in `Cheffile` rather than managing lots of cookbooks manually.

