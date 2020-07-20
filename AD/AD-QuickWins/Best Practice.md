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
Accounts no password required can be set with a blank password by a Domain Admin (Regular users do not have this right.) creating a massive hole in the security of the environment, with a free foothold to the threat actor.

https://activedirectoryfaq.com/2013/12/empty-password-in-active-directory-despite-activated-password-policy/
https://evotec.xyz/fixing-active-directory-passwordnotrequired-with-powershell/


# LAPS Not Deployed
Lorem Ipsum

# Reversible Encryption

Allows an attacker with appropriate access to retrieve the plaintext version of an account's password. This adds to the attack surface of the environment. 


https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/store-passwords-using-reversible-encryption

# *Much* More to come

I plan on splitting time between this and development on the Quick-Wins script, with the culminating goal of them complementing each other.
