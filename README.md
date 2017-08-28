## External DNS Servers block on IPFire 2.19 - Core Update 112 & Unbound 1.6.3

Before we get started, this guide assumes you already have a standard network setup with both RED and GREEN networks created, up and working.

This guide will be split based on sections. So without further ado let’s get started.

`- Service Groups`

1) As first step you would need to log into your IPFire web panel, hover over *Firewall* and select *Firewall Groups*.

2) In *Firewall Groups* you will need to select *Service Groups*, in *Add new service group* give it a group name and in *Remark* add something that will remind you of what this group service does, once than that hit *Add*.

3) On the next page in the *Add* selection you will need to select *DNS TCP* and click on *Add*. Do the same but this time select *DNS UDP*.

![Alt text](https://raw.githubusercontent.com/psammarco/IPFire-external-DNS-block/master/examples/1_service-groups.png "Service Groups")

`- Firewall Rules`

1) From within the IPFire web panel, hover over *Firewall*, select *Firewall Rules*, and select *New Rule*.

2) In *Source* select *Standard networks* and choose *GREEN*.

3) In *Destination* select *Standard networks* and choose *RED*.

4) In *Protocol* you will need to select *- Preset -*, select *Service Groups*, choose *DNS TCP* and *DNS block*, and select *REJECT*.

5) In *Additional settings* you would want to select *Log* and *Active Rule*. 

6) Once done that, simply click on *Update*.

*NOTE: Repeat the same steps if you want to block external DNS server usage for UDP traffic.*

![Alt text](https://raw.githubusercontent.com/psammarco/IPFire-external-DNS-block/master/examples/red-dns-block1_.png "RED DNS block 1")

![Alt text](https://raw.githubusercontent.com/psammarco/IPFire-external-DNS-block/master/examples/red-dns-block2.png "RED DNS block 2")

`- Firewall Rules (Incoming Firewall Access)`

1) Assuming we are still inside the Firewall Rules page, you would want to select *New Rule* so that we can create our very last rule.

2) In *Source* select *Standard networks* and choose *Any*.

3) In *Destination* select *Firewall* and choose *GREEN*.

4) In *Protocol* select *- Preset -*, select *Service Groups* , choose *DNS TCP* and *DNS block*, and select *ACCEPT*.

5) In *Additional settings* you would want to select *Log* and *Active Rule*. 

6) Once done that, simply click on *Update*.

![Alt text](https://raw.githubusercontent.com/psammarco/IPFire-external-DNS-block/master/examples/green-dns-block1.png "GREEN DNS block 1")

![Alt text](https://raw.githubusercontent.com/psammarco/IPFire-external-DNS-block/master/examples/green-dns-block2.png "GREEN DNS block 2")

Congratulations. If you have followed these steps correctly and your configuration looks like mine (see screenshots), you should have successfully blocked external DNS server usage. 

What will happen if somebody is using external DNS server is simply that the browser will remain on a loop in a blank page waiting for the DNS server to reply.

Additionally, if you want to restrict IP’s and domains access you would want to combine this guide alongside with my [blocked hosts megalist](https://raw.githubusercontent.com/psammarco/Hosts-megalist-block-for-unbound/master/block.conf); [(please read more here)](https://github.com/psammarco/Hosts-megalist-block-for-unbound/blob/master/README.md), which will ensure that a good amount of websites containing spam, malware, viruses, ads etc will be blocked within the entire LAN.

Please feel free to share any thoughts or feedbacks you may have. 
