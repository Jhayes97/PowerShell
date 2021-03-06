# Kerberoasting 
Lorem Ipsum

Praise be Tim Medin

# Delinquent *krbtgt* Password

The krbtgt account is created when a new domain is created. Below are more resources explaining how Kerberos works as an identity authenticator, and certain attacks targetting a stale krbtgt password. It is strongly recommended to absorb all of the posted resources below, however in short in order to issue Kerberos tickets, there needs to be a security principle for the Domain Controller to validate each ticket. This, alongside a few other things, is the krbtgt password hash.
If the krbtgt hash is compromised, so likely is the entire AD environment. STIG Windows Server 2016 recommends resetting the password(s) every 180 days.

https://adsecurity.org/?p=483\

https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password

https://www.youtube.com/watch?v=kp5d8Yv3-0c

### Golden Ticket Attack
If complete Domain compromise is accomplished and the krbtgt NTLM hash stolen, an attacker can begin forging their own tickets. This is a powerful persistence method.

https://attack.stealthbits.com/how-golden-ticket-attack-works/

https://ired.team/offensive-security-experiments/active-directory-kerberos-abuse/kerberos-golden-tickets

### Changing The *krbtgt* Password
The password that you specify is not important, as the system will generate a "strong password" for the krbtgt account. These steps are considered the absolute lowest impact to production, although abundently slow.

1. Confirm prior to reset that the domain controllers are all replicating with the command "Repadmin /replsummary"
2. Reset the password of the krbtgt account one time

![alt text](https://github.com/Jhayes97/PowerShell/blob/master/src/img/krbtgtreset.PNG "Resetting the krbtgt password")

3. Wait out the lifetime of tickets in your environment (usually and likely 10 hours) 
4. As you can see above from the Microsoft KB, the krbtgt will actually store hashes and accept tickets for a password history of 2, meaning you will need to now reset the krbtgt password again.

https://adsecurity.org/?p=3458

# Kerberos Pre-Authentication Not Required

Also known as AS-REP roasting, your organization is in big trouble if this misconfiguration is present. The secondary sobriquet comes from the mix of Kerbe*roasting* and the second step seen below in the Kerberos protocol for generating tickets.
 
![alt text](https://github.com/Jhayes97/PowerShell/blob/master/src/img/Visio-KerberosComms.png "Praise Sean Metcalf")
*credit to the awesome team at ADSecurity.org for the graphic.*

Although not enabled by default, if enabled attackers can crack the hash of the account's password. An in-depth explanation and demonstration of exploiting the vulnerability with the impacket suite script GetNPUsers.py can be found by the very informational VbScrub at the link below.

https://www.youtube.com/watch?v=pZSyGRjHNO4


# Accounts With No Password Policy
Accounts with the no password required attribute can be set with a blank password by a Domain Admin (Regular users do not have this right.) creating a massive hole in the security of the environment, with a free foothold to the threat actor.

https://activedirectoryfaq.com/2013/12/empty-password-in-active-directory-despite-activated-password-policy/

https://evotec.xyz/fixing-active-directory-passwordnotrequired-with-powershell/

# Protected Users Group Not Being Utilized
Lorem Ipsum


# LAPS Not Deployed
Lorem Ipsum

# Reversible Encryption

Allows an attacker with appropriate access to retrieve the plaintext version of an account's password. This adds to the attack surface of the environment. 


https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/store-passwords-using-reversible-encryption

# Schema Admin Membership

Members of the Schema Admin group are able to Modify the Domain's Schema, which is the underlying structure for the Directory Service. Changes to the schema are so occassionally required that it is common threat-surface-reduction sense to leave this group empty unless actively modifying the schema. By default, only the built in Domain Admin account is in this group. Were lingering accounts in this group to be compromised, forest restoration would become much more involved.

https://docs.microsoft.com/en-us/services-hub/health/remediation-steps-ad/remove-all-members-from-the-schema-admins-group-unless-you-are-actively-changing-the-schema

# Accounts with Passwords that never expire
Lorem Ipsum

# Delegation
Lorem Ipsum

### Constrained Delegation
Lorem Ipsum

### Unconstrained Delegation
Lorem Ipsum


# Legacy Operating Systems
Lorem Ipsum

# Domain-Functional Level
Lorem Ipsum
# Group Managed Service Accounts/Managed Service Accounts
Lorem Ipsum


# Limiting Domain Admin Count
Reducing the attack surface of your organization is key in the security lifecycle. Making certain that user/service accounts don't have more permissions than needed for operations is a necessary foundation for a mature AD environment. Sean Metcalf does a great dissection about the powercreep vendors tend to take when listing account requirements in the blog post below. 

https://adsecurity.org/?p=4115

# Microsoft's Administrative tier-model
Lorem Ipsum

# GPP Hacking
Lorem Ipsum

https://blog.rapid7.com/2016/07/27/pentesting-in-the-real-world-group-policy-pwnage/

# *Much* More to come

I plan on splitting time between this and development on the Quick-Wins script, with the culminating goal of them complementing each other.
