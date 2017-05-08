>That sounds way better. I am hoping to set this up. Do you know where I can find a checklist or aggregation of modern guide about specific implementations? I know a lot of the tech involved but not the specific products.

Mostly, I recommend channeling everything through GnuPG and running hardware for that. You'll have issues if you try to simultaneously use something like PKCS#11 for your SSH agent but GnuPG for other tasks. I document using GnuPG for SSH in [my desktop config repo](https://github.com/davidstrauss/desktop-configuration/blob/master/README.md), including hardware.

There are guides to creating an offline, software-managed root key and then signing the hardware tokens with that, but I prefer to just manage a set of hardware tokens instead. The hierarchical approaches only solve direct GnuPG usage, anyway, not SSH.
 
>My secrets include gpg keys, ssh keys, possibly a keepassx key depending on how I decide to do that. I need to check that. Right now I memorize more passwords than is probably advisable.

You can centralize all three needs (and more) on GnuPG with a hardware token:
GnuPG keys will obviously work as expected when backed with compatible hardware (instead of just software). My repo above explains basic setup from initializing hardware tokens to setting up new machines/installations to use existing tokens.
You'll want to move your SSH client to using the agent provided by GnuPG. This will require you to upload SSH public keys generated from your GnuPG keys. My repo above explains the rest, including auto-starting the GnuPG agent.
For passwords, I use [Password Store](https://www.passwordstore.org/). This supports encrypting/decrypting with GnuPG and synchronizing repositories over git, which you can do using git+ssh to leverage the previous work.
For mobile password access, NFC-compatible GnuPG tokens (and USB if you're willing to use a dongle) can decrypt entries in hardware on Android devices. For Android's git+ssh access, I just use an SSH key resident on my phone. Hardware tokens aren't yet supported for SSH on Android, but Password Store doesn't depend on repository access for password security, anyway.
For Google, GitHub, and Dropbox (and other U2F-supporting services), I use a YubiKey (which can also provide a combination of GnuPG hardware and NFC, depending on model).
So, in short, I can nearly run my whole crypto stack in hardware with one YubiKey Neo or any U2F key plus a Sigilance card (my laptop has a smart card reader). The only thing I don't have working yet is backing my browser client certificates with a GnuPG agent.
