# What is Terraform 
Terraform allows you to manage your AWS, and other cloud infrastructure, the same way you would manage servers using configuration management products like CFEngine or Puppet. Terraform is idempotent and convergent so only required changes are applied.



## Quick start

Note: these Terraform templates create real resources in your AWS account. The resources are part of the [AWS Free
Tier](https://aws.amazon.com/free/), but if you've used up all your credits, they may cost you money.

1. Install [Terraform](https://www.terraform.io/).
2. Add your AWS credentials as the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
3. Run `terraform plan`.
4. If the plan looks good, run `terraform apply`.


## Making changes

Try making some changes to the template to learn about basic Terraform features, as described in the following sections.

### Use a variable

Variables make your templates configurable. To become familiar with variables, try defining one in `main.tf`:

```hcl
variable "name" {
  description = "The name of the EC2 instance"
}
```

Next, use that variable in the `tags` of the `aws_instance`:

```hcl
resource "aws_instance" "example" {
  // ...

  tags {
    Name = "${var.name}"
  }
}
```

Try running `terraform plan` and `terraform apply` to see what happens.

### Use dependencies

Terraform resources can depend on each other. Terraform will automatically build a dependency graph and ensure the
resources get created in the right order. For example, to add an IP address to the EC2 instance, you can define an
`aws_eip` resource:

```hcl
resource "aws_eip" "example" {
  instance = "${aws_instance.example.id}"
}
```

Notice how the `instance` parameter is set to `"${aws_instance.example.id}"`. This is dependency on the `id` attribute
of the `aws_instance` you've already created. Terraform now knows that when you `apply` these templates, it needs to
create the `aws_instance` first, pull out its `id`, and then it can create the `aws_eip`.

## Cleaning up

To clean up the resources created by these templates, just run `terraform destroy`.



# I whipped up this example to build:

An SSH public key to be installed on the created EC2 instance.
A security group allowing HTTP and HTTPS.
A security group allowing SSH.
A tc2.micro EC2 instance with the above applied to it.
The 'provider' part of the file indicates to terraform to use its AWS provider with the given credentials. If you know AWS at all the terraform code is not hard to follow.

Create a file in your current directory called demo.tf. When you run terrafrom it searches the current directory for .tf files and reads them according to your instructions. For example:

```
provider "aws" {
   access_key = "your_key_here"
   secret_key = "your_secret_here"
   region = "us-east-1"
}

resource "aws_key_pair" "neptune" {
   key_name = "neptune"
   public_key = "ssh-rsa AAA removed for brevity 1XCr neil@neptune"
}

resource "aws_security_group" "ssh" {
   name = "ssh"
   description = "Allow inbound ssh"
   ingress = {
      from_port = 0
      to_port   = 22
      protocol  = "tcp"
      cidr_blocks = [ "0.0.0.0/0" ]
   }
}

resource "aws_security_group" "http" {
   name = "http"
   description = "Allow inbound http"
   ingress = {
      from_port = 0
      to_port   = 80 
      protocol  = "tcp"
      cidr_blocks = [ "0.0.0.0/0" ]
   }
   egress = {
      from_port = 0
      to_port   = 80
      protocol  = "tcp"
      cidr_blocks = [ "0.0.0.0/0" ]
   }
   egress = {
      from_port = 0
      to_port   = 443
      protocol  = "tcp"
      cidr_blocks = [ "0.0.0.0/0" ]
   }
}

resource "aws_instance" "tfdemo" {

    ami = "ami-60b6c60a"
    instance_type = "t2.micro"

   key_name = "it-admin"
   security_groups = [ "ssh", "http", "default" ]
}
```

- Terraform plan will report what must be done, but perform no changes.
- Terraform apply will make the changes shown above.
- Terraform show will show the current state.
- Terraform destroy will destroy everything that is defined.

* Note that there seems to be a built in order in which terraform runs that is not related to the order of the file. This is much like normal ordering in CFEngine. For example, when I run this code with nothing configured in AWS, it will try to build the server instance first, but fails because the groups and keys are not yet defined. But the groups and keys will be created next, so, run terraform a second time and it will converge, by creating just the instance while leaving the already existing groups and keys as they are.

