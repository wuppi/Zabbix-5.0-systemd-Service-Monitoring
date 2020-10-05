# Zabbix-5.0-systemd-Service-Monitoring
Monitoring running status of a single given Linux systemd.service (Debian 10-tested)

This is a simple Template for monitoring a systemd Service on a client.

Preconditions:

- Zabbix Server (I have 5.0)
- Zabbix Agent2 on the client (This is most important!)
- Systemd - Service up and running on the client

Description:

The Zabbix-Agent2 allows to directly monitor systemd Services. This template uses this feature so there is no need to install anything beyond zabbix-agent2 on the client.
It does not require any particular configuration on the client.

The template is configured to monitor a sample service alles primus.service.

You may want to adopt this prior uploading the template to the server.
To do so, please open the XML-File with your prefered editor and replace all occurances of "primus" with your desired service name.

The "mission critial part" is the correct naming of the service. In order to check this, please check upfront on a server console with

# zabbix_get -s &lt;client-ip&gt; -k systemd.unit.info&lsqb;"&lt;servicename&gt;",SubState&rsqb;
with <client-ip> being the ip or address of your client running the systemd-Service and <servicename> being the service name of the service to be monitored.

Watch out: My service is called primus while the required service name is primus.service
sample (not real domain  xyz.de)
zabbix_get -s xyz.de -k systemd.unit.info&lsqb;"primus.service",SubState&rsqb;
The result of the call should be "running".

The template can ce imported straight into the server by "Template" "Configuration" "Import"

After that, please assign the template to the host(s) you desire to monitor.

In order to check the template, simply stop the systemd service on the client

# systemctl stop <service>

After a while you should receive an alert.

Start the service again

# systemctl start <service>

and receive the email short after with a resolved- information.

Please note, this is my first template and it is not the greatest you could imagine. However, I was looking for this and I couldn't find working solutions in the net.

Have fun.
