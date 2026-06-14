**Suspicious Activity Investigation Lab**

**Suspicious Activity Investigation Lab:** Network artifacts extracted from packet capture data were ingested into Splunk Enterprise and analyzed to identify external hosts, cloud infrastructure, local devices, multicast traffic, and unusual communications through dashboards, reports, alerts, detections, and threat-hunting investigations.

**Creating Index**

Index: suspicious

Description: Create a dedicated index for suspicious network activity investigations.

Please refer to image # 1 in the repository.

**Uploading Dataset**

Dataset: suspicious_connections.log

Settings:\
Index: suspicious\
Host: MacBookPro\
Sourcetype: suspicious_activity

Description: Ingest suspicious network artifacts extracted from packet capture analysis.

Please refer to images # 2 and 3 in the repository.

**Verifying Ingestion**

Query: index=suspicious\
\
Or\
\
source="suspicious_connections.log" host="MacBookPro" index="suspicious" sourcetype="suspicious_activity"

. Was the suspicious activity dataset successfully ingested into Splunk?\
Yes

Please refer to image # 4, and 5 in the repository.

**Verifying Event Count**

Query:

index=suspicious\
\| stats count

. How many suspicious activity events were ingested?

The suspicious activity dataset was successfully ingested into Splunk. The dataset contains **1 event**, which includes **15 lines of network artifacts and connection information** extracted from packet-capture analysis.

. How many network artifacts are available for investigation?

Although Splunk reports 1 event, the event contains 15 individual network artifacts, including hostnames, device names, router-related activity, multicast traffic, and external cloud-hosted systems. These artifacts provide multiple investigation points for threat-hunting and network analysis.

Please refer to image # 6 in the repository.

**Reviewing Suspicious Activity Data**

Query:

index=suspicious\
\| table \_time host sourcetype \_raw

. What network artifacts are present in the dataset?

g3100.mynetworksettings.com\
ec2-3-221-141-237.compute-1.amazonaws.com\
igmp.mcast.net\
all-systems.mcast.net\
macbookpro\
iphone\
Reply is-at\
Request records

These artifacts represent router communications, cloud-hosted infrastructure, multicast activity, local devices, and network discovery traffic.
\
. What hosts, domains, and devices are available for investigation?\
\
Hosts and Domains

g3100.mynetworksettings.com\
ec2-3-221-141-237.compute-1.amazonaws.com\
igmp.mcast.net\
all-systems.mcast.ne

Devices

macbookpro\
iphone

The investigation identified local devices, router-related services, multicast network traffic, and communications involving an Amazon AWS cloud-hosted system. The most notable artifact is ec2-3-221-141-237.compute-1.amazonaws.com, which represents an external cloud-hosted service and warrants additional review to determine the nature of the communication. The multicast entries (igmp.mcast.net and all-systems.mcast.net) are commonly associated with local network service discovery and group communications.

Please refer to image # 7 in the repository.
\
**Identifying External Host**

Query: index=suspicious amazonaws

. Which external hosts communicated with the environment?\
\
ec2-3-221-141-237.compute-1.amazonaws.com. This hostname is associated with an Amazon AWS EC2 cloud server and was observed communicating with macbookpro.59061

. Are any cloud-hosted systems present in the dataset?\
\
Yes. The dataset contains the cloud-hosted system: ec2-3-221-141-237.compute-1.amazonaws.com which is an Amazon AWS EC2 instance.

The investigation identified communication between a local device (macbookpro) and an Amazon AWS EC2 host (ec2-3-221-141-237.compute-1.amazonaws.com) over HTTPS. Cloud-hosted systems are common on modern networks, but external communications should be reviewed to determine whether they are expected application traffic or require additional investigation.

Please refer to image # 8 in the repository.

**Identifying Local Devices**

Query: index=suspicious macbookpro OR iphone

\
. Which local devices were observed on the network?

Macbookpro
iphone
\
. Were any user devices discovered during the investigation?

Yes. The investigation discovered two user-device artifacts:

macbookpro
iphone

Please refer to image # 9 in the repository.

**Identifying Router Activity**

Query: index=suspicious mynetworksettings

. Was router-related activity observed?

Yes. Router-related activity was observed through the hostname:

g3100.mynetworksettings.com


. Which network infrastructure devices were identified?

g3100.mynetworksettings.com
igmp.mcast.net\
all-systems.mcast.net

Analyst Assessment

The investigation identified router-related communications (g3100.mynetworksettings.com) and multicast network infrastructure services (igmp.mcast.net and all-systems.mcast.net). These artifacts are commonly associated with local network management, device discovery, and multicast communications. No evidence of malicious router activity was observed within this dataset.

Please refer to image # 10 in the repository.
 
**Identifying Multicast Activity**

Query: index=suspicious mcast

. Was multicast traffic observed in the environment?

Yes. The investigation identified multicast-related traffic within the dataset through the following entries:

igmp.mcast.net\
all-systems.mcast.net

. Which multicast services were detected?

igmp.mcast.net
all-systems.mcast.net
\
Analyst Assessment

The investigation identified multicast traffic associated with igmp.mcast.net and all-systems.mcast.net. These services are commonly used for local network communication, device discovery, and multicast group management. The observed multicast activity appears consistent with normal local network operations and does not indicate malicious behavior within\
this dataset.

Please refer to image # 11 in the repository.

**Visualization**

Query:\
\
index=suspicious
\| stats count

. How many suspicious activity artifacts are currently being monitored?

The visualization shows 1 suspicious activity event currently being monitored. There are 15 Network Artifacts.
\
. What is the total volume of suspicious activity records?

The dataset contains 1 ingested event. Examination of the event reveals multiple network artifacts, including local devices, router-related activity, multicast services, and an external cloud-hosted system. 15 Network Artifacts.

Please refer to images # 12 and 13 in the repository.

**Report**

Query: index=suspicious

. What suspicious network artifacts were identified during the investigation?

g3100.mynetworksettings.com\
ec2-3-221-141-237.compute-1.amazonaws.com\
igmp.mcast.net\
all-systems.mcast.net\
macbookpro\
iphone

These artifacts represent router-related activity, an external AWS cloud-hosted system, multicast services, and local devices observed in the dataset.

. Which findings should be documented for future analysis?

ec2-3-221-141-237.compute-1.amazonaws.com
g3100.mynetworksettings.com\
igmp.mcast.net\
all-systems.mcast.net\
macbookpro\
iphone

Analyst Assessment

The investigation identified communications involving a local workstation, a mobile device, router-related services, multicast network services, and an external Amazon AWS EC2 host. The most notable finding was communication with ec2-3-221-141-237.compute-1.amazonaws.com, which should be retained for future review and correlation with other network activity. The remaining artifacts appear related to normal local network communication and device discovery.

Please refer to images # 14 and 15 in the repository.

**Dashboard**

Query:

index=suspicious\
\| stats count

Dashboard Name:

Suspicious Activity Dashboard

. What suspicious activity indicators are currently available for monitoring?

The dataset currently contains one suspicious activity event for monitoring. Within this event, several network artifacts were identified, including local devices, router-related services, multicast services, and an external cloud-hosted system.

. What network artifacts make up the current investigation dataset?

macbookpro\
iphone\
g3100.mynetworksettings.com\
ec2-3-221-141-237.compute-1.amazonaws.com\
igmp.mcast.net\
all-systems.mcast.net\
\
The dashboard displays one suspicious activity event containing multiple network artifacts. The dataset includes local devices (macbookpro, iphone), router-related services (g3100.mynetworksettings.com), multicast services (igmp.mcast.net, all-systems.mcast.net), and an external AWS cloud-hosted system (ec2-3-221-141-237.compute-1.amazonaws.com) available for investigation and monitoring.

Please refer to image # 16 in the repository.

**Alert**

Query: index=suspicious amazonaws

Alert Name:

Suspicious External Host Detection

. Has potentially suspicious network activity been detected?

Yes. The investigation identified communication involving the external cloud-hosted system:

ec2-3-221-141-237.compute-1.amazonaws.com

This external communication was observed between:

macbookpro.59061 ↔ ec2-3-221-141-237.compute-1.amazonaws.com.https

. Are there findings requiring analyst review?

Yes. The following finding warrants analyst review:

ec2-3-221-141-237.compute-1.amazonaws.com

Please refer to images # 17 and 18 in the repository.

**Detection Rule**

Query: index=suspicious amazonaws OR mcast\

. Can unusual external communications be automatically detected?

Yes. The detection rule successfully identified communications involving:

ec2-3-221-141-237.compute-1.amazonaws.com

as well as multicast-related traffic:

igmp.mcast.net\
all-systems.mcast.net

These communications can be automatically detected through Splunk searches, alerts, and detection rules.


. Are cloud-hosted external systems present in the dataset?

Yes. The dataset contains the following cloud-hosted external system:

ec2-3-221-141-237.compute-1.amazonaws.com

which is an Amazon AWS EC2 host observed communicating with:

macbookpro.59061

Analyst Assessment

The detection rule identified communication with an external Amazon AWS EC2 host and multicast network services. The AWS EC2 host represents the most notable external communication observed in the dataset and should be reviewed to determine whether the activity is expected. The multicast services (igmp.mcast.net and all-systems.mcast.net) are commonly associated with normal local network discovery and group communication activity.

Please refer to image # 19 in the repository.

**Threat Hunting**

Query:

index=suspicious\
\| table \_time host sourcetype \_raw

. Which external hosts require additional investigation?

The primary external host requiring additional investigation is:

ec2-3-221-141-237.compute-1.amazonaws.com

This host is an Amazon AWS EC2 system observed communicating with:

macbookpro.59061

. What network artifacts appear unusual or unexpected?

The most unusual artifacts identified were:

ec2-3-221-141-237.compute-1.amazonaws.com\
(oui Unknown

The AWS EC2 host represents external cloud communication, while the unknown OUI entries could not be fully resolved from the packet-capture artifacts.


. Are there cloud-hosted systems communicating with local devices?

Yes. The investigation identified communication between:

macbookpro.59061

and

ec2-3-221-141-237.compute-1.amazonaws.com

indicating communication between a local device and an Amazon AWS cloud-hosted system.


. What findings could warrant further network analysis?\
\
ec2-3-221-141-237.compute-1.amazonaws.com\
g3100.mynetworksettings.com\
(oui Unknown

These artifacts involve external cloud communications, router-related activity, and unresolved network identifiers that may benefit from additional investigation and correlation with other network logs.

Please refer to images # 20 and 21 in the repository.
\
Analyst Assessment

Threat-hunting analysis identified local devices (macbookpro, iphone), router-related activity (g3100.mynetworksettings.com), multicast services (igmp.mcast.net, all-systems.mcast.net), and communication with an Amazon AWS EC2 host (ec2-3-221-141-237.compute-1.amazonaws.com). The AWS EC2 host represents the most significant external communication observed in the dataset and should be reviewed to determine whether the activity is expected. The remaining artifacts appear consistent with local network operations and device discovery activity.


