# wazuh_decoders
wazuh configurations that works

#Wazuh Kasperky Security Center integration 

We are going to export all malware events that kasperky generates to a Syslog server that runs Wazuh Agent.

#working with Syslog RFC5424
Why? - because you can export in this format even if you don't have the superior license for Endpoint Protection

The way to the clouds:
Using a syslog (rsyslog) to write log files from KSC and the Wazuh Agent sending then to Wazuh 

![image](https://user-images.githubusercontent.com/37113825/231496646-61d863b7-4c0f-4f59-ab07-cfb3d0683943.png)

Because Kasperky syslog is way too indistinguishable, the only way that a I got to work out was to create a template in Rsyslog:

IN Rsyslog server:
1- modify the /etc/rsyslog.conf
2- create a logrotate in /etc/logrotate.d/rsyslog, to maintain space
3- systemctl restart rsyslog.service

IN wazuh agent:
1- modify the /var/ossec/etc/ossec.conf, to make the agent read the syslog archive
2- systemctl restart wazuh-agent

IN Wazuh server:
1- create the decoder
2- create the rules
3- systemctl restart wazuh-manager

The files in this repo contains an explanation for each one of them. 
