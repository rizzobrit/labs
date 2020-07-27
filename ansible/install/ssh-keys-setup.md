### create a user on all machines ( controller & all targets )

	useradd ansible -m -d /home/ansible -s /bin/bash

### add user to sudoers for root previliges  on all machines ( all targets )

	echo -e 'ansible  ALL=(ALL)  NOPASSWD:  ALL' > /etc/sudoers.d/ansible

### genereate ssh keys for above user on contrller machine 

```
	1) switch to user ( su - ansible )
	2) run "ssh-keygen" command as user ( this will genereate ssh keys for the user ) 
	#ansible@ip-172-31-43-67://usr/bin$ run ssh-keygen
	#
	#
	ansible@ip-172-31-43-67://usr/bin$ ./ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ansible/.ssh/id_rsa):
Created directory '/home/ansible/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ansible/.ssh/id_rsa.
Your public key has been saved in /home/ansible/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:ICqrL28qFnactd/ibAC06V3gjOsem1+6/pWLigHYZbw ansible@ip-172-31-43-67
The key's randomart image is:

```

### copy user ssh keys from ansible contrller to all target hosts

```
	1) on ansible controller machine
		cd /home/ansible/.ssh 
		cat id_rsa.pub (copy the content)
```
```
	2) on all taget machines
		   swith to the user ( su - ansible )
		   mkdir -p /home/ansible/.ssh
		   touch /home/ansible/.ssh/authorized_keys
		   chmod 600 /home/ansible/.ssh/authorized_keys
		   vi /home/ansible/.ssh/authorized_keys  (enter the copied contet of id_rsa.pub from controller & save the file)
```	
	

