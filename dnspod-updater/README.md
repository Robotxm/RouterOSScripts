# DNSPoed Updater for RouterOS

Original script from [https://github.com/arho14/dnspod-ros](https://github.com/arho14/dnspod-ros). Modified to support IPv6.

## Configuration Example

```
# PPPoE interface name (for IPv4)
:local pppoe "pppoe-out1"

# IPv6 pool name (for IPv6)
:local ipv6pool "ipv6-pool"

# DNSPod Token (Format: <ID>,<Token>. Example: 123456,1a2b3c4d5e6f7890)
:local token "123456,1a2b3c4d5e6f7890"

# Domain (Example: example.com)
:local domain "example.com"

# Subdomain(s) for IPv4 (Format: "<Subdomain1>";"<Subdomain2>";"<Subdomain3>". Example: "www";"home")
:local subdomains4 {"www";"home"}

# Subdomain(s) for IPv6 (Format: "<Subdomain1>";"<Subdomain2>";"<Subdomain3>". Example: "www";"home")
:local subdomains6 {"www";"home"}
```

## Usage

1. Goto System -> Scripts tab and click the add icon.
2. Enter the name of scripts like `dnspod-updater`. It will be used later.
3. Paste the content of `dnspod-updater` in this repository into the Source field. Modify the content under `Configuration` section. Then click OK to save.
4. Goto PPP -> Profiles tab and click the add icon.
5. Under General tab enter the name of profile like `pppoe-client-update-dnspod-ip`.
6. Under Scripts tab enter the content below into the On Up field, where `dnspod-updater` is the name of script you entered in step 2.

```
delay 5s
:execute "dnspod-updater"
```

7. Click OK to save.
8. Goto Interface tab and double click the interface you want to use as the address source. Under Dial Out tab select the profile you created in step 5 from the dropdown menu of Profile.
9. Click OK to save. **Note that the connection will be interreupted and then re-establish.**
10. Goto Log, you will see items like `Update A record for [home.example.com] successfully. New IP: 1.2.3.4`.