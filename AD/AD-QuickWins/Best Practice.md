# Delinquent krbtgt password

The krbtgt account is created when a new domain is created. Below are more resources explaining how Kerberos works as an identity authenticator, and certain attacks targetting a stale krbtgt password. It is strongly recommended to absorb all of the posted resources below, however in short in order to issue Kerberos tickets, there needs to be a security principle for the Domain Controller to validate each ticket. This, alongside a few other things, is the krbtgt password hash.
If the krbtgt hash is compromised, so likely is the entire AD environment.

https://adsecurity.org/?p=483\

https://docs.microsoft.com/en-us/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password

https://www.youtube.com/watch?v=kp5d8Yv3-0c

## Golden Ticket Attack
If complete Domain compromise is accomplished and the krbtgt NTLM hash stolen, an attacker can begin forging their own tickets. This is a powerful persistence method.

https://attack.stealthbits.com/how-golden-ticket-attack-works/

https://ired.team/offensive-security-experiments/active-directory-kerberos-abuse/kerberos-golden-tickets

## Changing the krbtgt password


# More to come

I plan on splitting time between this and development on the Quick-Wins script, with the culminating goal of them complementing each other.
