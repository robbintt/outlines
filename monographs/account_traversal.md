# Account Traversal 

**Disclaimer: This document does not include a strict howto.**

Can someone who has gained control of your **phone number** take over all your online accounts?

What if someone controls one of these:
1. Primary Email
2. Recovery Email for the Primary Email
3. Domain Name Registrar - for the Domain Name of your Primary Email


## Can I Trust my phone company?

No, that's how the [CIA Director got hacked](https://www.wired.com/2015/10/hacker-who-broke-into-cia-director-john-brennan-email-tells-how-he-did-it/).

If you need more fear, watch this [exploit demo video](https://youtu.be/bjYhmX_OUQQ).

Not convinced? This reporter [lost it all](https://www.wired.com/2012/08/apple-amazon-mat-honan-hacking/) (and [got some back](https://www.wired.com/2012/08/mat-honan-data-recovery/)).


## Should I turn off `phone number recovery`?

I don't know, should you?

This whole document is dedicated to convincing you that you should, unless you don't have the bandwidth to do so.

Removing `Phone Number Recovery` from primary accounts will help a lot, but it's also the default way that you recover your account if you lose your password. It is not the only way though, and we will explore better alternatives.

Most accounts are dependent on one of the following accounts:
- Google Account (parent account of gmail service)
- iCloud Account (Apple)
- Facebook Profile
- Phone Number (Provider Managed Account)
  
  
### But I'm in a hurry!

First of all, if you aren't really thinking about these problems and how they affect your online presence, you should just leave phone recovery on. Turning it off requires attention, consideration, and light maintenance.

If you are in a position that could compromise your `salary`, `business`, `community`, or `family`, think carefully about whether you govern your information in a way that impacts those relationships fairly.


### Determine if you have what it takes!

If you are disorganized, lose your keys often, or have things stolen often, the recovery phone number may be safer for you.


## Clarifying 2FA and FIDO-U2F

FIDO-U2F provides key marginal benefits over using Google Authenticator.

TL;DR - The benefits are marginal, tangible, and convenient.


### Which product do I use?

I used the [Yubico FIDO-U2F](https://www.amazon.com/dp/B00NLKA0D8). You will need to register two of them on each account and put one in a safe place in case you lose the other.

### Benefits

1. Fast compared to OTP 2FA (one-time password e.g. Google Authenticator)
2. Immune to Shoulder Surfing (no visual acquisition vector)
3. Phone theft happens daily, this is not in a phone
4. A `backup FIDO-U2F` is cheaper & easier to maintain than a `backup phone` containing additional Google Authenticator OTP for each account.
    - Many OTP setups only support one linked app, too (needs fact checked)
5. The `account server` may be able to detect a `man in the middle attack` or a `phishing website`
    - However, many companies may not bother doing this -- shame on them
    - Cannot verify they are doing this or doing it right
    
### Costs

1. **Surprise:** You have to use Google Authenticator on each account if you want to login to things on an iPhone
    - Apparently you can connect the FIDO-U2F dongle to an android phone?
    - Browsers: FIDO-U2F only works with Chrome and Opera (for now) 
        - Reportedly Firefox and Microsoft are coming
    - No hope for Safari, iPhone FIDO-U2F (Apple hates sharing)
    - You have to use Google Authenticator for everything else
2. Make a backup U2F token in case you lose your keys
3. Keep your backup up-to-date
    - Maintain an index of what services use U2F so you can audit your backup

### Improving Security without FIDO-U2F?

The same order of account protection can be achieved without FIDO-U2F:
1. Use Google Authenticator
2. Have a second BACKUP 2FA method (NOT a phone number)
    - **WHEN your phone is stolen**, you WILL lose all those Google Authenticator 2FA tokens.
    - iPhone **Encrypted** backups currently store them. This isn't guaranteed.
    - Unencrypted backups do not store them. I do not know if icloud backups store them.
3. Disable Phone Number Account Recovery


## Know your `recovery emails` and `recovery phone numbers`

Google has a recovery email feature. Is it your Yahoo account from 2003?

If your recovery email for tons of services is Google, and your recovery email for Google is hacked, then you are a `sitting duck`. Change your recovery email!

Did you know that yahoo is [totally compromised](https://www.nytimes.com/2017/03/17/technology/yahoo-hack-data-indictments.html?_r=0)?

A customer service agent at a phone company often has the power to reallocate your phone number to a new device.   If a person `steals your identity`, they can compromise any accounts with a `recovery phone number`.



## Building an `account recovery graph`

It is helpful to build a graph of how your account dependencies resolve. This requires you to list out your commonly accessed accounts.

Draw this graph with bubbles and arrows.

For each account ask yourself, "if I lose the password for this account, how do I recover it?"  The answer is usually traced back to one `recovery phone number` and a few `recovery email` accounts.

Once you find your most common `recovery emails` and `recovery phone numbers`, ask yourself - how do you recover those accounts?  You should find that everything depeonds on one or two things, often your `phone number` and `primary email`.

Now imagine if a thief got access to one of these `recovery accounts`. What happens next? How many accounts can they steal from you?


### Does your `primary email` have a `recovery email`?

Why would you have a recovery email on your primary email?  If that recovery email is compromised, it is at the top of your `account recovery graph`, and a prime target for an attacker.


### Know your Circular Dependencies

If your Google and iCloud accounts both recover each other, they form a closed loop and can compromise any account linked to either one.


### Account Traversal

This just means the ability to walk down your whole graph from one piece of information. This is how you lose all your data.

Account traversal generally begins at your email or phone number.

For a given online account, a person can probably access your `recovery email` if they control your `recovery phone number`.
