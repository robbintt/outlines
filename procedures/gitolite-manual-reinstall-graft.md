## Gitolite Migration

Instructions for migrating gitolite3 to a new host.


### Gitolite `gitolite-admin` management

If gitolite-admin is managed remotely, it simply needs the `git remote` path changed.

If gitolite-admin is managed locally, ensure the old `admin.pub` key is kept as it is committed in the repo.


### Graft gitolite3 install onto a server and change your admin key

This process assumes you are doing a key change in your admin repo concurrent with reinstall.

If you do not need to do a keychange and keep `gitolite-admin` remote then the only thing you have to do is install gitolite through `apt` and graft the replacement directory. Much faster.

There may be an easier way, LMK if you try one. This method is intended to graft the magic, whole hog, rather than try to integrate new magic on top.


1. `ssh-keygen` - have a local key for easy gitolite install
1. `apt-get install gitolite3`
    - Do a default setup and DO point it to your local pubkey: `/home/<user>/.ssh/id_rsa.pub`
    - this pubkey is going to get wiped out anyways
1. Move the generated keys (from `ssh-keygen`) to temporary files
    - I like to put them in `/home/<user>` for now
1. Add the old keys where the generated keys were
    - This ensures  you will be able to push to your grafted repository
    - `id_rsa`, id_rsa.pub`
1. Copy the original gitolite-admin management repo to the new host
    - The git remote can be set as localhost if it is managed locally
1. Delete the gitolite management repo on the new host `/var/lib/gitolite3`
1. Copy the original gitolite installation directory to the new host `/var/lib/gitolite3`
    - Chown the gitolite installation directory to `gitolite:gitolite`
1. You should be able to `git fetch` with no issues
1. Add the new key to the gitolite-admin repository
    - Replace `gitolite-admin/keydir/admin.pub` with your new `id_rsa.pub`
    - Push this commit
1. Replace the old keys in `.ssh` with the generated keys
