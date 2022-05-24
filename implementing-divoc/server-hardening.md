# Server Hardening

This is the minimum list of hardening and other steps that need to be performed to secure the Linux server containing the DIVOC platform. The assumption is that the installation happens on a bare metal setup. While the concepts remain the same, the methodology might differ for commercial cloud setups.&#x20;

## Check for open ports

* Identifying open connections to the internet is a critical mission.

{% hint style="info" %}
netstat -antp
{% endhint %}

* Once you have identified the open ports, you can stop/purge the applications which keep unnecessary ports open.&#x20;
* The only acceptable open ports are 22 and 443. Access to the other ports outside the Kubernetes network should be prohibited.&#x20;
* All ingress should be routed through 443 port only as needed.

## **Secure SSH**&#x20;

SSH is secure, but we need to harden this service as well. If we can disable SSH, then the problem solved. However, if we want to use it, we have to change the default configuration of SSH. Password**-**based authentication should be disabled and only key-based authentication should be allowed. The steps for creating sudo users with public and private keys are as follows:

* Create a non root sudo user

{% hint style="info" %}
adduser \<user>
{% endhint %}

* Add the user to sudo users group

{% hint style="info" %}
usermod -aG sudo \<user>
{% endhint %}

* Login to the machine as the user

{% hint style="info" %}
su - \<user>
{% endhint %}

* Create SSH directory with appropriate permissions

{% hint style="info" %}
mkdir -p $HOME/.ssh\
chmod 0700 $HOME/.ssh
{% endhint %}

* Generate a key pair for the protocol, and run:

{% hint style="info" %}
ssh-keygen -t ed25519 -C "My key for DIVOC server"
{% endhint %}

* Share the public key created with users you expect to connect to the server

{% hint style="info" %}
$HOME/.ssh/id\_ed25519.pub
{% endhint %}

* You can modify your SSH configuration to be more secure by performing the following changes to the configuration file:

{% hint style="info" %}
nano /etc/ssh/sshd\_config
{% endhint %}

* Make sure that root cannot login remotely through SSH

{% hint style="info" %}
PermitRootLogin no
{% endhint %}

* Allow some specific users

{% hint style="info" %}
AllowUsers \[username]
{% endhint %}

* Enable public key-based authentication and disable password-based authentication

{% hint style="info" %}
PubkeyAuthentication yes\
PasswordAuthentication no
{% endhint %}

* There are some additional options that must exist in the “sshd\_config” file: MaxAuthTries 5
* Finally, set the permissions on the sshd\_config file so that only root users can change its contents:

{% hint style="info" %}
chown root:root /etc/ssh/sshd\_config

chmod 600 /etc/ssh/sshd\_config
{% endhint %}



_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
