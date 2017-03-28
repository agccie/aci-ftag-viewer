# aci-ftag-viewer
Check the FTAG topology in an ACI fabric

This script builds and validates all forwarding trees (FTAG) within all on pods on a Cisco ACI fabric. From the ACI managed information tree (MIT), it collects required isis, lldp, and fmcast objects to verify per-node status matches the expected value.  Additionally, the script prints the logical tree to help understand the path for multicast/broadcast/unknown uncast traffic. 

To begin, upload the script to the APIC directory. Then execute the script with optional filters.
For example:
```
apic1# ./aci_ftag_viewer.py --help
usage: aci_ftag_viewer.py [-h] [--debug {debug,info,warn,error}]
                          [--offline OFFLINE] [--offlineHelp] [--ftag FTAG]
                          [--pod POD]

Check the FTAG topology in an ACI fabric

optional arguments:
  -h, --help            show this help message and exit
  --debug {debug,info,warn,error}
                        debug level
  --offline OFFLINE     Use this option when executing the script on offline
                        data. If not set, this script assumes it is executing
                        on a live system and will query objects directly.
  --offlineHelp         print further offline help instructions
  --ftag FTAG           tree/ftag to verify (default all)
  --pod POD             pod to verify (default all)

apic1# ./aci_ftag_viewer.py --ftag 3


################################################################################
#  Pod 1 FTAG 3
#  active nodes: 32, inactive nodes: 0
################################################################################
node-1002
  +- 2/23 ------- 1/50 node-211
  +- 2/24 ------- 1/50 node-212
  |                      +- 1/49 ------- 2/32 node-1001
  |                                             +- 2/30 ------- 1/50 node-2005
  |
  +- 2/18 ------- 1/53 node-221
  +- 2/15 ------- 1/49 node-222
  +- 2/7 -------- 1/50 node-231
  +- 2/1 -------- 1/50 node-232
  +- 2/12 ------- 1/50 node-241
  +- 2/14 ------- 1/50 node-242
  +- 2/5 -------- 1/50 node-251
  +- 2/21 ------- 1/50 node-252
  +- 2/22 ------- 1/50 node-261
  +- 2/6 -------- 1/50 node-262
  +- 2/8 -------- 1/50 node-271
  +- 2/10 ------- 1/50 node-272
  +- 2/9 -------- 1/50 node-281
  +- 2/13 ------- 1/50 node-282
  +- 2/11 ------- 1/98 node-291
  +- 2/17 ------- 1/98 node-292
  +- 2/3 -------- 1/50 node-1111
  +- 2/2 -------- 1/50 node-1122
  +- 2/4 -------- 1/50 node-1134
  +- 2/19 ------- 1/50 node-1156
  +- 2/20 ------- 1/50 node-1178
  +- 2/16 ------- 1/50 node-1199
  +- 2/28 ------- 1/30 node-2000
  +- 2/26 ------- 1/54 node-2001
  +- 2/25 ------- 1/53 node-2002
  +- 2/36 ------- 1/51 node-2003
  +- 2/35 ------- 1/50 node-2004


Pod 1 FTAG 3: all nodes reachable on tree
```
