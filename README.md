# freebsd_openvpn_ansible

A simple ansible playbook to get you openvpn running on FreeBSD 11 in a few seconds.

## Requirements:
* FreeBSD 11 up and running
* Your ssh public key must be on the server 
* Ansible installed

## You may want to:
* Place your **server ip address** inside the **inventory** file.
* Change variable values inside the **vars** directory. (especifically **openvpn_server_ip** and **iface_name**)
* Make sure your firewall allows udp traffic on port 1194
* If you are using a virtualized machine with a virtual iface you need to run **ifconfig <iface-name> -tso4 -tso6 -vlanhwtso -lro -txcsum -rxcsum** once the ansible playbook has finished running and possibly everytime the machine reboots. Instead you can pass these parameters inside the rc.conf file and not worrry about it.

## Generating the client.conf file
1) cd /usr/local/etc/openvpn/easy-rsa
2) ./easyrsa.real build-client-full client_name nopass
3) cat /usr/local/etc/openvpn/easy-rsa/pki/ca.crt
4) place the contents of ca.crt between the <ca> </ca> tags inside
client_template.conf
5) cat /usr/local/etc/openvpn/easy-rsa/pki/issued/client_name.crt
6) place the contents of client_name.crt between the <cert> </cert> tags inside
client_template.conf
7) cat /usr/local/etc/openvpn/easy-rsa/pki/private/client_name.key
8) place the contents of client_name.key between the <key> </key> tags inside
client_template.conf
9) Send the client_template.conf to the client machine and have fun (:


