footer: _© Zendesk, 2015_ - Cassiano Aquino - caquino@zendesk.com
slidenumbers: true
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
#[FIT]CHEF🍲
#[FIT]TASTING

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Zendesk automation 
## in numbers (Sunday Feb 22 2015)

- 1823 nodes
- 169 roles
- 182 cookbooks
- ~ 87,500 daily convergences 
- ~ 685,000 lines of code / data
- ~ 27,000,000 attributes

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
#[FIT]WHY
#[FIT]AUTOMATION?

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
##Infrastructure
###Should be

![right,15%](http://imagesci.com/img/2013/04/snowflake-background-8906-hd-wallpapers.png)

- Repeatable
- Testable
- Scalable
- **NO SPECIAL SNOWFLAKES**

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# ALSO
- It's impossible to manage 1800 servers manually
- without getting insane.

![right](http://blog.stackoverflow.com/wp-content/uploads/sysadminday.jpg)

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
#[FIT]WHY
#[FIT]CHEF?

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)

# Automations archeology 🗿

![250%, inline](http://cfengine.com/wp-content/uploads/2014/06/logo_with_box.png)![100%, inline](http://puppetlabs.com/wp-content/uploads/2010/12/PL_logo_horizontal_RGB_sm.png)![180%, inline](https://upload.wikimedia.org/wikipedia/en/thumb/5/56/Chef_Software_Inc._company_logo.png/400px-Chef_Software_Inc._company_logo.png)

* 1993 - CFEngine
* 2005 - Puppet
* 2007 - Zendesk
* 2009 - Opscode Chef


---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# CFEngine 

```
package:
	"nginx"
		package_policy => "add",
		package_method => "apt"
```

## Well, looks cool but how do I start?

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
## Puppet

```
package { 'nginx':
	provider=>'apt',
	ensure=>'installed'
}
```

## This looks easier, I think I can do it!

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# CHEF

```
package "nginx" do
	action :install
end
```
- As a bonus let's manage the service

```
service "nginx" do
	action [ :enable, :start ]
	supports :reload => true
end
```

# HEY, I KNOW THIS!

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# YES! IT'S RUBY

![right](http://www.necolt.com/assets/technologies/ruby-847c4d5e8e43981d3690e77fe389124d.png)

- Uses a Ruby DSL and pure Ruby
- Data is stored in JSON
- Templates are **erb files**
- Community
2.023 Cookbooks 
61.320 Chefs

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Learning curve

![inline](http://thelearningcurve.ca/wp-content/tlcimages/gartnerhypecycle.jpg)

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# What Chef is?

- A configuration management system
- An API for your infrastructure
- A **searchable** catalog of attributes
- Arbitrary datastore of global JSON data, also **searchable**.
- Client / Server architecture

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Behind the scenes

* erlang
* nginx
* redis
* rabbitmq
* solr
* postgresql
* couchdb

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Main components
## Nodes

- Physical, Virtual or Cloud machine that's managed by a chef-client.

## node configuration itens

- Attributes and a run_list

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Configuration item
## Attributes

- Key / Value
- Automatic and Manual
- **Searchable!** 🔍

```
knife search node 'zendesk_config_pod:4 AND zendesk_config_hostgroup:voice' -i
voice1.pod4.sac1.zdsys.com
voice2.pod4.sac1.zdsys.com
voice3.pod4.sac1.zdsys.com
voice4.pod4.sac1.zdsys.com
```
---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Attributes
## Automatic

**Examples**
- How many CPU's the node have?
- How much memory the node have?
- What are the node IP addresses?
- **Immutable attributes!**

### OHAI ✋
- Detect and populate attributes about your OS.

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Attributes
## Manual

**Examples**
- In which POD this server is?
- What projects are deployed to this server?
- Whatever key/value needed

**Where?**
- Attribute Files, Node, Recipe, Environment, Role

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# run_list

- Settings to configure a node into a desired state.
- Ordered list of roles and/or recipes/cookbooks

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Configuration units

### Grouping: 
- Environments 
production, qa, staging...
- Roles
web, db, lb...
- Nodes
server1.mydomain.com...
- Attributes
kernel.release: 2.0.36 (yikes! this is not true!)

^^
Environment map an organization’s real-life workflow
Roles are functionality group or configuration group

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Main components
## Cookbooks 📕
- fundamental unit of configuration and policy distribution.
- defines a scenario.
- all of the components that are required to support that scenario.

^ scenario: everything needed to install and configure MySQL
components: Attributes, Files, Recipes, Resources, Providers, Templates, Versions, Metadata

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Cookbook 📕

- How do I write my first cookbook?

## IDEA 💡
### Let's write our first cookbook!
- Install nginx
- Adds an "static" index file

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# Cookbook 📕
## Index file content

- Hostname and main IP address
- Memory
- Number of CPU's
- OS, distribution, distribution name and kernel Version
- Configurable message

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
#[FIT]DEMO TIME

---
![](http://blog.iso50.com/wp-content/uploads/2009/07/bsod.jpg)

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
#Why ::File?

- Chef has its own classes named File
- We want the Ruby's File class

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
# NEXT STEPS

- Full chef basics class (~ 5:00 hours of duration)
- Feeling adventurous? 
http://github.com/caquino/chef-class
Vagrant lab and presentation

---
![](http://d16cvnquvjw7pr.cloudfront.net/www/img/p-brand/mentor-bg-2X.png)
#[FIT]THANKS
### http://syshero.org - @syshero
### http://github.com/caquino
### caquino@zendesk.com
