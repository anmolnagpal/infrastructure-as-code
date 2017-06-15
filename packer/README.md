# About Packer
An open source product from HashiCorp called “Packer” is a tool for managing your machine templates as defined by a JSON file. At first glance you might think, “Why would I need to manage my templates as a JSON file? They don’t change much so who cares?” But in reality, these templates are getting trickier to keep track of than they used to be. Organizations are now venturing more and more into public cloud spaces as well as keeping their on-premises vSphere environments, and they’ll need templates in each location which could result in template sprawl and version inconsistencies.

# Using Packer

Leveraging Packer allows you to build a new template based on an existing image, which could be a great way to patch templates with new updates, add additional functionality in your base images, keep templates identical in multiple clouds, and best of all, store your image as a piece of code in your version control repository.

The basic process for using Packer includes taking an old template or Amazon machine image, applying new patches or software to it, and creating a new template or AMI from the results of those two actions. The original template is unharmed and a newly versioned template is created.

![alt text](https://github.com/anmolnagpal/infrastructure-as-code-training/blob/master/images/img1.png)

The result of using Packer across multiple environments means that through a single process, you can manage multiple templates to ensure consistency.

![alt text](https://github.com/anmolnagpal/infrastructure-as-code-training/blob/master/images/img2.png)

Simply managing templates may be a first step with Packer. Once you’ve matured this process, you can use Packer to build images on the fly and deploy the image with a tool like Terraform to build an immutable deployment infrastructure, which takes out all of the manual build steps that cause drift. Using Packer, you can be sure of a consistent deployment every time and if you need to build a new workload, you can create a new Packer build. Packer can be a great tool for use in blue-green deployment models, too. This deployment method can also be augmented with CI/CD tools like Jenkins to deploy templates, unit test capabilities, and then deployment into production.


### Reference:
- https://www.packer.io/docs/index.html
