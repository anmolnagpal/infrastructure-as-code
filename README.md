# Infrastructure-as-code (IAC)

A long time ago, in a data center far, far away, an ancient group of powerful beings known as sysadmins used to deploy infrastructure manually. Every server, every route table entry, every database configuration, and every load balancer was created and managed by hand. It was a dark and fearful age: fear of downtime, fear of accidental misconfiguration, fear of slow and fragile deployments, and fear of what would happen if the sysadmins fell to the dark side (i.e. took a vacation). The good news is that thanks to the DevOps Rebel Alliance, we now have a better way to do things: Infrastructure-as-Code (IAC).
Instead of clicking around a web UI or SSHing to a server and manually executing commands, the idea behind IAC is to write code to define, provision, and manage your infrastructure. This has a number of benefits:

- You can automate your entire provisioning and deployment process, which makes it much faster and more reliable than any manual process.
-  You can represent the state of your infrastructure in source files that anyone can read rather than a sysadmin’s head.
- You can store those source files in version control, which means the entire history of your infrastructure is now captured in the commit log, which you can use to debug problems, and if necessary, roll back to older versions.
- You can validate each infrastructure change through code reviews and automated tests.
- You can create reusable, documented, battle-tested infrastructure packages that make it easier to scale and evolve your infrastructure.
- There is one other very important, and often overlooked, reason for why you should use IAC: it makes developers happy. 

Deploying code is a repetitive and tedious task. A computer can do that sort of thing quickly and reliably, but a human will be slow and error prone. Moreover, a developer will resent that type of work, as it involves no creativity, no challenge, and no recognition. You could deploy code perfectly for months, and no one will take notice — until that one day where you mess it up.That creates a stressful and unpleasant environment. IAC offers a better alternative that allows computers to do what they do best (automation) and developers to do what they do best (coding).



## [Ansible](./ansible/README.md)

Ansible is an open source IT configuration management and automation tool. Similar to Puppet and Chef, Ansible has made a name for itself among system administrators that need to manage, automate, and orchestrate various types of server environments. Unlike Puppet and Chef, Ansible is agentless, and does not require a software agent to be installed on the target node (server or switch) in order to automate the device. By default, Ansible requires SSH and Python support on the target node, but Ansible can also be easily extended to use any API.

![alt text](images/img8.png)

## [Packer](./packer/README.md)

An open source product from HashiCorp called “Packer” is a tool for managing your machine templates as defined by a JSON file. At first glance you might think, “Why would I need to manage my templates as a JSON file? They don’t change much so who cares?” But in reality, these templates are getting trickier to keep track of than they used to be. Organizations are now venturing more and more into public cloud spaces as well as keeping their on-premises vSphere environments, and they’ll need templates in each location which could result in template sprawl and version inconsistencies.

![alt text](images/img1.png)

## [Terraform](./terraform/README.md)

Terraform allows you to manage your AWS, and other cloud infrastructure, the same way you would manage servers using configuration management products like CFEngine or Puppet. Terraform is idempotent and convergent so only required changes are applied.
