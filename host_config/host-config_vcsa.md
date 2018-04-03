<!--
host_config/host-config_vcsa.md
-->

If you need to flush the DNS cache of the vCenter Server Appliance:

systemctl restart dnsmasq<br>
systemctl restart systemd-resolved.service

This is necessary if your DNS cache has an incorrect entry or you recently changed an A record and rather not wait for the vCSA cache to time out on it's own.
