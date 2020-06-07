# enom-ddns

EdgeOS dhclient-script to support enom DDNS

This shell script is meant to be run from within the [dhclient-script](http://manpages.ubuntu.com/manpages/focal/en/man8/dhclient-script.8.html) ecosystem on [EdgeOS](https://dl.ubnt.com/guides/edgemax/EdgeOS_UG.pdf).

Otherwise, it operates like most DynamicDNS (DDNS) protocols: when DHCP binds, renews, or rebinds a public IP address,
this code will update the Enom entry for the current hostname. Note that Enom defaults to using the IP address of the
incoming connection -- you can modify the script to add an `&Address=...` option to the URL.

## INSTALLATION

1. Open the EdgeOS CLI and navigate to `/etc/dhcp/dhclient-exit-hooks.d`
1. Use any available text editor to generate the [`enom-ddns`](enom-ddns) file.
1. Make sure to set the `DOMAIN` and `PASSWORD` values appropriately.

## TESTING

To run manually:

1. Open the EdgeOS CLI and navigate to `/etc/dhcp/dhclient-exit-hooks.d`.
1. Run `reason=RENEW . enom-ddns`.
1. Examine contents of `/tmp/enom-ddns.log` to check for success or failure.
1. Verify that `[...EdgeOS hostname...].[...Enom domain...]` resolves to correct IP.
