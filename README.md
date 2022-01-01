# Unattended Upgrades for Zcash on Debian

The `zcash` package provides `zcashd` which has "End-of-Support Halt": the node halts at a given block height. This is to signal that the Electric Coin Co does not maintain that version beyond that height, and it prompts users to re-opt-in to a new zcash node, either a more recent `zcashd` provided by ECC, or an alternative node. This reinforces blockchain governance by forcing users to decide which node to upgrade to, which becomes crucial if there are competing consensus rule upgrades released.

The downside is operational headache, since infrastructure operators must track the EOS Halt schedules and upgrade their nodes on that schedule.

Some users may want to permanently opt-in to future ECC `zcashd` releases as soon as they are released and don't want the headache of tracking EOS Halt schedules. Using Debian's `unattended-upgrades` system is an easy way to do this. This document describes how to configure a Debian system to automatically upgrade to the latest ECC `zcash` release.

## Setup Instructions

### Install ECC Zcashd

[zcashd debian installation reference](https://zcash.readthedocs.io/en/latest/rtd_pages/install_debian_bin_packages.html)

```
sudo apt-get update && sudo apt-get install apt-transport-https wget gnupg2
```

```
wget -qO - https://apt.z.cash/zcash.asc | gpg --import
```

```
gpg --export 3FE63B67F85EA808DE9B880E6DEF3BAF272766C0 | sudo apt-key add -
```

Verify the key fingerprint listed on the reference page. By verifying it against that page, you are ensuring you use the package signing key set by the owner of the `readthedocs.io` account (or anyone controlling that site).

```
echo "deb [arch=amd64] https://apt.z.cash/ stretch main" | sudo tee /etc/apt/sources.list.d/zcash.list
```

```
sudo apt-get update && sudo apt-get install zcash
```

```
zcash-fetch-params
```

### Configure Debian Unattended Upgrades

[debian unattended-upgrades reference](https://wiki.debian.org/UnattendedUpgrades)

Steps:

```
# apt-get install unattended-upgrades apt-listchanges
```

```
# editor /etc/apt/apt.conf.d/50unattended-upgrades
```

**FIXME: incomplete**
