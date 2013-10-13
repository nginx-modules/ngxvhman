ngxvhman
========

A collection of tools to automate virtual host administration for nginx.

Boring stuff:
	(c) Copyright
	Author:		Maximilian 'cyrusol' Pfeifer, cyrusol@secure-mail.cc
	Date:		2013-10-13
	License:	MIT
	Version:	1.0

=============================================================================

Included are:
	ngxvhadd <USER> <SQLPASSWORD>	Adds a new vhost
	ngxvhdel <USER>			Deletes a vhost
	ngxvhen	<USER>			Enables a vhost
	ngxvhdis <USER>			Disables a vhost

=============================================================================

Requirements:
	nginx
	mariadb / mysql
	openssh

=============================================================================

Preparations:

1. Prepare the chroot directory:
	mkdir /home/jail

2. Prepare the skel directory:
	mkdir /root/vhost
	mkdir /root/vhost/public

3. Prepare openssh for chrooted sftp
	Append following lines to sshd_config:

	Match Group vhost
		AuthorizedKeysFile	/home/vhost/%u/.ssh/authorized_keys
		ChrootDirectory		/home/vhost/%u
		AllowTcpForwarding	no
		X11Forwarding		no
		ForceCommand		internal-sftp

	or change them according to your needs.
	If your openssh is too old to support AuthorizedKeysFile in
	a Match block, consider the AuthorizedKeysFile2 global option.

4. Write your nginx vhost configs and save them at
   /etc/nginx/sites-available/vh-<USER>.
