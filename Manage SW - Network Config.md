lab08 

==🟢*The objective of this lab is to master core Linux administration tasks by managing network profiles and static IP routing via the nmtui interface, and performing manual repository configuration. You will gain hands-on experience in software management by deploying packages from third-party sources while troubleshooting common repository connectivity issues in a Red Hat environment.*== 

**Linux Administration Lab Section 1: Network Configuration**  
1. Find your active interface name and the Default Gateway of your system.
   
   `samah@localhost:~$ ip -br address show`
		%%lo               UNKNOWN        127.0.0.1/8 ::1/128
		ens160           UP             192.168.17.130/24 fe80::20c:29ff:fea0:94e1/64 %%
		

3. Open nmtui and create a new Ethernet connection named "network-lab".
4. Configure the profile with a static IP ending in .22/24 (within your current network range).
5. Set the DNS server to 8.8.8.8.

6. Activate the "network-lab" connection using the nmtui menu.
7. Verify that the interface now displays the new IP address using the command line.
   
	`$ip a`
		%%1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000==
	    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00==
	    inet 127.0.0.1/8 scope host lo==
        valid_lft forever preferred_lft forever==
	    inet6 ::1/128 scope host noprefixroute==
        valid_lft forever preferred_lft forever
		2: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
	    link/ether 00:0c:29:a0:94:e1 brd ff:ff:ff:ff:ff:ff
	    altname enp3s0
	    altname enx000c29a094e1
	    inet 192.168.17.22/24 brd 192.168.17.255 scope global noprefixroute ens160
        valid_lft forever preferred_lft forever %%
   
	`$ nmcli connection show`
		%%NAME       UUID                                  TYPE      DEVICE 
		network_lab  11938ca6-57df-4d5e-925c-e9f495573855  ethernet  ens160 
		lo           0abedc80-6f1c-433a-9ad3-9333daacb5c6  loopback  lo     
		ens160       57be3bb3-969e-3c70-a221-b960a95b56e6  ethernet%%


**Section 2: Package Management (Manual Repository)**
 1. Create a repository file named /etc/yum.repos.d/epel.repo.
 2. Manually add the configuration for the EPEL 10 repository using the following URL: https://dl.fedoraproject.org/pub/epel/10/Everything/x86_64/. 
3. Ensure the repository is enabled and GPG check is disabled.
   
	`~$ sudo vim /etc/yum.repos.d/epel.repo` 
	`~$ sudo cat /etc/yum.repos.d/epel.repo`

		%%[AppStream]
		name=Red Hat Enterprise system App Stream  
		baseurl=https://dl.fedoraproject.org/pub/epel/10/Everything/x86_64/
		enabled=1
		gpgcheck=0%%

5. Install the 7zip package while disabling all other repositories during the installation process.
   
		`~$ sudo dnf install 7zip --disablerepo="*" --enablerepo="AppStream"`

			%%Installed:
			  7zip-26.04-1.el10_3.x
              Complete!%%

7. Verify the installation by running the 7zz command
   
		`~$ 7z`

		 %%7-Zip 26.04 (x64) : Copyright (c) 1999-2026 Igor Pavlov : 2026-10-05
		  64-bit locale=en_US.UTF-8 Threads:128 OPEN_MAX:524288 %%






