# Okuninushi
My personal repo for using ClearML. This contains scripts and docs to remind me of how to spin up agents, the ClearML Server, and etc.


# First steps when starting a new VM

First you should interact as an admin user on root directory.

```bash
sudo su
cd
```

Then, update and upgrade your system.

```bash
apt-get update -y
apt-get upgrade -y
```


# To install Docker

You need Docker if you want to deploy the Clearml Server or if you want to spin a ClearML Agent with access to a private repo (using SSH keys) or if you want to have a VM serving a model with ClearML Serving.

To install docker (for Ubuntu 20.04 TLS amd), this guide always worked for me: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04.


# To deploy the ClearML Server

The VM must allow HTTP and HTTPS connections. The official tutorial is very useful: https://clear.ml/docs/latest/docs/deploying_clearml/clearml_server_linux_mac.


# To spin up a ClearML Agent with SSH keys.

For this, you must have docker installed, as you must launch the agent in docker mode. 
First, you must start a SSH Agent.

```bash
ssh-agent -s
```

Then you must export the two variables shown

```bash
export SSH_AUTH_SOCK=<SSH_AUTH_SOCK>
export SSH_AGENT_PID=<SSH_AGENT_PID>
```

Then you must create a SSH key.


```bash
ssh-keygen -t rsa
```

After that, you must add this key to the SSH Agent

```bash
ssh-agent add ~/.ssh/id_rsa
```

Lastly, to spin up the ClearML Agent, you must run it on dokcer mode.


```bash
clearml-agent daemon --queue <queue to listen> --detached --cpu-only --docker
```

Finally, you must add the public key generated to the private repo. Copy paste the output of

```bash
cat ~/.ssh/id_rsa.pub
```
