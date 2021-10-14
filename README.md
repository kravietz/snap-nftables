[![nftables-pk](https://snapcraft.io/nftables-pk/badge.svg)](https://snapcraft.io/nftables-pk)


# Nftables Snap package

Provides the latest version of [nftables](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page)
command-line utility with the intention of replacing outdated and buggy packages
provided by mainline Linux distributions. You can install this package from the Snap Store:

    snap install nftables-pk

As well as create a system-wide alias:

    snap alias nftables-pk.nft nft

Remember to update your nftables scripts to point to `/snap/bin/nft` which is the new location of the `nft` binary.

As the program does not have access to the system-wide `/etc` directory, configuration files are expected
to be located in `/var/snap/nftables-pk/common`.

Simplest usage example - put your `nftables` configuraton in `/var/snap/nftables-pk/common/nftables.conf` and run:

    nft -f /var/snap/nftables-pk/common/nftables.conf
    nft list ruleset
    
Because the `/var/snap/nftables-pk/common` is mapped, you can also load the same file as:
    
    nft -f /etc/nftables.conf
    nft list ruleset
    
Any other file from that directory - e.g. `/var/snap/nftables-pk/common/other.conf` can be loaded as follows:

    nft -f /etc/nftables/other.conf
    nft list ruleset

See [nftables](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page) for documentation and examples. 

## Build

    git clone git@bitbucket.org:kravietz/snap-nftables.git
    cd snap-nftables
    snapcraft
    
The snap runs in full confinement which means it does not have access to general operating system files and
kernel interfaces used to configure nftables by default. If installed from Snap Store, these should be automatically
connected. If you're building it on your own, you need to connect them after installation: 

    snap install --dangerous nftables-pk_v0.9.1_amd64.snap
    snap connect nftables-pk:firewall-control
    snap connect nftables-pk:network-control




