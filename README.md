<h1 align="center"> Wazuh Decoders for Kaspersky (syslog) </h1>
wazuh configurations that works

<h4 align="center"> 
    :construction:  Project in development  :construction:
</h4>
<h3>Wazuh Kasperky Security Center integration</h3> 

We are going to export all malware events that kasperky generates to a Syslog server that runs Wazuh Agent.

<h4>working with Syslog RFC5424</h4>
Why? - because you can export in this format even if you don't have the superior license for Endpoint Protection

<h4>The way to the clouds:</h4>
Using a syslog (rsyslog) to write log files from KSC and the Wazuh Agent sending then to Wazuh 

![image](https://user-images.githubusercontent.com/37113825/231496646-61d863b7-4c0f-4f59-ab07-cfb3d0683943.png)

Because Kasperky syslog is way too indistinguishable, the only way that a I got to work out was to create a template in Rsyslog:

In Rsyslog server:
<ol>
  <li>modify the <code>/etc/rsyslog.conf</code></li>
  <li>create a logrotate in <code>/etc/logrotate.d/rsyslog</code>, to maintain space</li>
  <li>systemctl restart rsyslog.service</li>
</ol>

In wazuh agent:
<ol> 
  <li>modify the <code>/var/ossec/etc/ossec.conf</code>, to make the agent read the syslog archive</li>
  <li>systemctl restart wazuh-agent</li>
</ol>

In Wazuh server:
<ol>
  <li>create the decoder</li>
  <li>create the rules</li>
  <li>systemctl restart wazuh-manager</li>
</ol>

The files in this repo contains an explanation for each one of them. 

![image](https://user-images.githubusercontent.com/37113825/231562580-10689b95-d156-41a7-87be-f894f2a60b00.png)

