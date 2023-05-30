---
sidebar_position: 30
sidebar_label: Router
title: Create new router
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## 2.2 Login and Update the repo and apps on VM

<Tabs
  defaultValue="DigitalOcean"
  values={[
      { label: 'Digital Ocean', value: 'DigitalOcean', },
      { label: 'Azure', value: 'Azure', },
      { label: 'AWS', value: 'AWS', },
      { label: 'Google Cloud', value: 'GCP', },
  ]}
>
<TabItem value="GCP">

Once the VM is created, we can login through SSH

</TabItem>
</Tabs>

## 2.7 Route Table 
<Tabs
  defaultValue="DigitalOcean"
  values={[
      { label: 'Digital Ocean', value: 'DigitalOcean', },
      { label: 'Azure', value: 'Azure', },
      { label: 'AWS', value: 'AWS', },
      { label: 'Google Cloud', value: 'GCP', },
  ]}
>
<TabItem value="GCP">

For any router setup as local gateway (i.e. local-er in test network 2), you will need to setup routes in GCP.

Following is an example route for intercepting traffic destined for the IP: 11.11.11.11/32. The next hop is our local gateway ER.

Following are the route table entries in Non-openziti-client
-	To reach the destination IP 11.11.11.11/32
-	To reach the destination 100.64.0.0/10 which is the locally resolved DNS IP by the Ziti DNS 


![Diagram](/img/GCP/7.RouteTableforNonzitiClient.JPG)

Note: In GCP, I gave the name of the instance as openziti-private-er-vm for the local gateway which is same as local-er in test network 2


</TabItem>
</Tabs>

## 2.8 Source and Destination Check
<Tabs
  defaultValue="DigitalOcean"
  values={[
      { label: 'Digital Ocean', value: 'DigitalOcean', },
      { label: 'Azure', value: 'Azure', },
      { label: 'AWS', value: 'AWS', },
      { label: 'Google Cloud', value: 'GCP', },
  ]}
>
<TabItem value="GCP">

In GCP, the "Source and Destination Check" is named **IP forwarding**

In the VM configuration screen, choose the **ADVANCED OPTIONS** & under the **NETWORKING** section (like the picture below). **Enable** the **IP forwarding**

![Diagram](/img/GCP/8.IPForwardingPrivateER.JPG)

</TabItem>
</Tabs>

## 2.9 Firewall
<Tabs
  defaultValue="DigitalOcean"
  values={[
      { label: 'Digital Ocean', value: 'DigitalOcean', },
      { label: 'Azure', value: 'Azure', },
      { label: 'AWS', value: 'AWS', },
      { label: 'Google Cloud', value: 'GCP', },
  ]}
>
<TabItem value="GCP">

GCP’S default firewall is blocking all incoming access to the VM.

Private router i.e. local-er in test network 2  was enrolled with edge listener and Tunneler enabled & following are the inbound firewall requirements for the instance.


![Diagram](/img/GCP/9.FWforPrivateER.JPG)

•	TCP Port 22 is opened only for the SSH access to the VM
•	UDP Port 53 is opened for accepting the DNS query request from the Non-openziti-client

Also allow HTTP Traffic to flow via the Private router i.e. local-er in test network 2 originated from the Non-openziti-client

![Diagram](/img/GCP/10.AllowHTTPinPrivateER.JPG)

Inbound firewall requirements for the Public Edge router


![Diagram](/img/GCP/11.FWforPublicER.JPG)




</TabItem>
</Tabs>
