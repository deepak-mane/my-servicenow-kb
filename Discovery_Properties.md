# Discovery Properties
## Discovery settings

1. In case the VIPs (Load Balancer Virtual Services) did not return as part of the SNMP Probe payload, fire the SHH Probe. 
- Yes

2. When doing IP-based discovery against a given host, also run probes that retrieve AWS EC2 metadata.
- Yes

3. Enforce unique IP addresses: if set to yes, then each time a computer, printer, or network gear is discovered, and that device has a valid IP address, then any other devices with the same IP address have their IP address field cleared.
- No

4. When doing IP-based discovery against a given host, also run probes that retrieve Azure metadata.
- Yes

5. Use JSON for IP ranges in Shazzam: If "yes", discovery will encode Shazzam's IP ranges as JSON, dramatically reducing the payload size.
- Yes

6. Enforce syncing of IP addresses: if set to yes, then each time a computer is discovered, and that device has multiple NICs, one of the IP addresses associated with the NICs will be chosen as the IP Address field of the CI.
- Yes

7. Always update host name: If "yes", discovery will always update the host name with the most recently discovered value contingent upon the source being trusted. Note that this may result in hand-entered values being overwritten.
- Yes

8. DNS or NetBIOS is trusted host name source: If "yes", trust the device name discovered via DNS or NetBIOS. If checked, CI's host name found via DNS or NBT will be used.
- No

9. SSH is trusted host name source: If "yes", trust the device name discovered via SSH. If checked, any device name found via SSH will be used instead of the name found by a reverse DNS lookup.
- No

10. WMI is trusted host name source: If "yes", trust the device name discovered via WMI. If checked, any device name found via WMI will be used instead of the name found by a reverse DNS lookup.
- No

11. SNMP is trusted host name source: If "yes", trust the device name discovered via SNMP. If checked, any device name found via SNMP will be used instead of the name found by a reverse DNS lookup.
- No

12. Include domain name in host name: If "yes", include the domain name as part of the host name. For example, "bosco.service-now.com" instead of "bosco".
- Yes

12. Host name case: If "Lower case" is selected, always translate the host name into lower case; if "Upper case" is selected, always translate the host name to upper case; if "No change" is selected, leave the host name intact. This primarily affects host names discovered with NETBIOS, though some non-standard DNS systems may also return some or all of the name in upper case.
- Lower case

13. Set OS domain name by NBT or WMI: If "yes", Windows domain name is set by NBT. Otherwise it is set by WMI.
- Yes

14. Discover software packages: Enable the discovery of software packages.
- Yes

15. Application mapping: Enable the application mapping portion of Discovery
- Yes

16. Active Processes Filter: Optimization for application dependency mapping. Filters the active processes returned by Discovery to only those that have a match in the Process Classification table.
- No

17. Save ECC queue attachments: The normal behavior for discovery sensors is to delete attachments to ECC queue entries upon successful sensor processing. Setting this property to "yes" overrides this behavior, and forces attachments to be preserved. This would normally only be useful for debugging purposes.
- Yes

18. BGP router exploration disable: Controls whether Network Discovery exploration of routers running the BGP protocol is disabled. Normally such exploration IS disabled because of the huge size of BGP routing tables, and because generally such routers are only operating at the edge of large networks where further network discovery would be irrelevant. The only time this value should be set to "no" is in the unlikely case that your organization uses BGP routers as edge routers between relatively small networks (such as between buildings on a single campus).
- Yes

19. CI identification debugging: if true, enables debug logging (into the CI Identification Log) for CI Identification.
- No

20. Network router selection method: This property controls the method used to decide (during Network Discovery) which router should be selected as the router to be associated with a given IP Network. The possible values are: "First Router" (the first router that discovers the network is associated), "Last Router" (the last router that discovers the network is associated), "Most Networks" (the router with the most attached networks is associated), and "Least Networks" (the router with the least attached networks is associated).
- Most Networks

21. Physical interface types: A comma-separated list of interface types that will be considered "physical" for the purposes of network discovery. In other words, if a router (or device capable of routing) has an interface of this type, the networks connected to that interface will be considered locally connected to that device. The default interface types include Ethernet, 802.11, and Token Ring types. Interface type numbers are defined in the SNMP MIB-2, specifically in OID 1.3.6.1.2.1.2.2.1.3.
- 6,117,9,71,209


22. Switch interface types: List of interface types (comma-separated) that will be considered Interface type numbers are defined in the SNMP MIB-2, specifically in OID 1.3.6.1.2.1.2.2.1.3. Devices with any interface types that do not appear in this list will be classified as routers (if they have routing capability). A complete list of the interface type numbers may be found on the IANA web site, in the section "ifType definitions".
- 7,8,9,26,53,62,69,71,78,115,117,209

23. Virtual interface types: List of interface types (comma-separated) that will be considered "virtual" for the purposes of network discovery. In other words, if a router (or device capable of routing) has an interface of this type, the networks connected to that interface will be considered virtually connected to that device. The default interface types include the propVirtual type. Interface type numbers are defined in the SNMP MIB-2, specifically in OID 1.3.6.1.2.1.2.2.1.3.
- 53

24. Network discovery debugging: Enables extensive logging of all Network Discovery activities on the instance.
- Yes

25. Maximum netmask size for discoverable networks (bits): The maximum number of bits in a regular netmask for networks that will be discovered by Network Discovery. By "regular netmask" we mean a netmask that can be expressed in binary as a string of ones followed by a string of zeroes (255.255.255.0 is regular, 255.255.255.64 is irregular). Regular networks are commonly expressed like this: 10.0.0.0/24, which means a network address of 10.0.0.0 with a netmask of 255.255.255.0. Larger bit numbers mean networks with smaller numbers of addresses in them. For example, the network 10.128.0.128/30 has four addresses in it: one network address (10.128.0.128), one broadcast address (10.128.0.131), and two usable addresses (10.128.0.129 and 10.128.0.130). Small networks like this are commonly configured in netowrk gear to provide loopback addresses or networks used strictly by point-to-point connections. Since these sorts of networks generally don't need to be discovered by Network Discovery, it would be useful to filter them out. By setting this property to a value of 1 through 32, you can limit the sizes of regular networks that are discovered. Setting it to any other value will cause all networks to be discovered. Irregular networks are always discovered. The default value is 28, which means that regular networks with 8 or fewer addresses will not be discovered.
- 28

26. Networks discovery functionality: the Functionality used to discover networks. Usually this should be "SNMP only".
- SNMP only

27. Log Message Length: Limit the maximum message length that will be displayed in Discovery Log table. A value of 0 or any negative number will disable this limit.
- 200

28. CPU speed rounding: Enter the number to round the CPU speed to. The units are in MHz. 
- 1

29. Memory rounding: Enter the number to round the computer RAM to. The units are in MB. 
- 1

30. IP service affinity: If "yes", IP service affinity will be enabled. IP service affinity allows Discovery to remember the last port of the IP address that was discovered.
- No

31. DNS Host Name And Domain Name Regex: The default parsing of FQDN (Fully Qualified Domain Name) is to pick the first name separated by dots as the host name and the rest of the names as the domain name. For example, "machine1.testlab.service-now.com" has host name of "machine1" and domain name of "testlab.service-now.com". The property allows regex with two capturing groups with the first group representing the host name and the second group the domain name.
- ``` ^([^.]+)\.((?:[^.]+\.)+[^.]+)$ ```

32. Use probe results cache: If set to yes, the cache will be checked to see if the results of the probe need to be processed by a sensor. It will only need to be processed if the results have changed from the last discovery run.
- No

33. Warn on Minor Version Mismatch: If "yes", warnings will be logged when minor_version mismatches are detected during Discovery sensor processing.
- No

34. Maximum concurrent invocations per schedule: Prevents an unbounded number of invocations from inundating the system when a schedule takes longer than the time between invocations. The value is an integer defining the maximum number of automated invocations of the same schedule that may proceed at one time. If the limit has been reached subsequent scheduled invocations will be cancelled. The default value is 3. A value of 0 or any negative number will disable this restriction.
- 3

35. Map servers and network devices to routers and layer-3 switches If the "L3 mapping" property is enabled, it will map servers and network gears to its associated routers and layer-3 switches
- Yes

36. Windows software is SCCM managed: If "yes", Discovery will not populate software for computer CIs also managed by SCCM.
- No

37. CMDB Identifiers: If "yes", identification and reconciliation will be handled by the CMDB API instead of through the old Discovery implementation. 
- Yes 

38. Enable configuration file tracking as part of the Pattern based Horizontal Discovery
- Yes 

39. File Tracking: Maximal file size for tracked configuration file content (B)
- 500000

40. File Tracking: Maximal number of tracked configuration files per CI
- 50

41. File Tracking: Time window in days for limiting the number changes on a tracked configuration file
- 7

42. File Tracking: Number of changes allowed on a tracked configuration file in the defined time window
- 4

43. For 7-Mode NetApp storage servers use native discovery instead of SMI-S
- Yes 

44. For Cluster Mode NetApp storage servers use native discovery instead of SMI-S
- Yes

45. ADME: Enable enhanced ADM probe. If "yes", the ADM Enhanced probe will be triggered and only fall back to the ADM probe as needed.
- No

46. ADME - Unix Base Dir: An existing directory on the target Unix machines to be used as a workspace. Must be a absolute path to the directory.
- /tmp

47. ADME - Windows Base Dir: A network share on the target Windows machines to be used as a workspace.
- admin$\temp

## END
