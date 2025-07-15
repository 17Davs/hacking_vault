   
### Authenticated vs. Unauthenticated Scans

Authenticated scans require the subject host's credentials and are more detailed than unauthenticated scans. These types of scans are helpful for discovering the threat surface within the host. However, unauthenticated scans are conducted without providing any credentials of the subject host. These scans help identify the threat surface from outside the host.

|Authenticated Scans|Unauthenticated Scans|
|---|---|
|The credentials of the subject host must be provided to the vulnerability scanner.|The vulnerability scanner does not require the host’s credentials; it only needs the IP address.|
|Identifies the vulnerabilities that can be exploited by the attackers having access to the host.|Identifies the vulnerabilities that can be exploited by an external attacker having no access to the subject host.|
|It provides a deeper visibility into the target system by scanning its configuration and installed applications.|It is less resource-intensive and straightforward to set up.|
|For example, scanning an internal database by providing its credentials to the vulnerability scanner.|For example, scanning a public-facing website for vulnerabilities that any user can exploit.|

### ![Authenticated Scans.](Hacking%20Vault/Attachments/a043f04cc8b54afb8ba7abde5b4d4bec.png)![Unauthenticated Scans..](Hacking%20Vault/Attachments/6645aa8c024f7893371eb7ac-1726737564579.png)

### Internal vs. External Scans

Internal scans are conducted from inside the network, while external scans are conducted from outside the network. Let's see a few of their differences below.

|Internal Scans|External Scans|
|---|---|
|Conducted from inside the network.|Conducted from outside the network.|
|It focuses on the vulnerabilities that can be exploited inside the network.|It focuses on the vulnerabilities that can be exploited from outside the network.|
|Identifies vulnerabilities that would be exposed to the attackers once they get inside the network.|Identifies the vulnerabilities exposed to the attacker from outside the network.|

![External vs Internal Scans.](Hacking%20Vault/Attachments/6645aa8c024f7893371eb7ac-1726737564755.png)

The choice between vulnerability scan types depends on several factors. Authenticated scans are often used for internal vulnerability scanning, while unauthenticated scans are mostly used for external vulnerability scanning.