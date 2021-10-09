# Using Ansible with AWS

This repo contains the code to go along with my YouTube video Using Ansible with AWS.

## Create a virtual environment

I *strongly* recommend using a virtual environment for all things ansible. There are few things worse than troubleshooting 
ansible for a few days only to learn that it was some unrelated package causing the problem (when your highschool sweetheart dumps
you being on that list). Using a virtual environment ensures you control dependencies plus makes this whole thing portable.

```shell
python3 -m venv .env
source .env/bin/activate
```

## Install dependencies

Install the python dependencies needed, including ansible.

```shell
pip install -r requirements.txt
```

## Configure dynamic inventory

We'll use the [ansible inventory role for communicating with AWS](https://github.com/ansible-collections/amazon.aws/blob/main/docs/amazon.aws.aws_ec2_inventory.rst).

`ansible-galaxy collection install amazon.aws`

This requires an inventory file. Modify `aws_ec2.yaml` to match your environment as needed.

## Check it out

For this to work, you need an AWS Access Key and AWS Secret Access Key. The also must be configured to work with your 
system. See [this](https://docs.aws.amazon.com/cli/index.html) for additional info.

Now we can get an inventory of our AWS environment:

`ansible-inventory -i aws_ec2.yaml --graph`

## Targeting hosts

You can also target specific hosts based on tag names:

`aws tag_Role_webserver -i aws_ec2.yaml -m ping`

will connect to all EC2 instances with a tag named `Role` that has a value of `webserver`

## Using playbooks

You can now configure EC2 instances using ansible playbooks that you create, or downloaded from [Ansible Galaxy](https://galaxy.ansible.com/home).

For additional details, check out the accompanying video on the DevOps for Developers [YouTube](https://youtube.com/devopsfordevelopers) channel.
