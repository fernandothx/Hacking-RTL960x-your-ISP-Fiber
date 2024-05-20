# ODI DFP-34X-2C2
1. This for stick using Realtek `RTL9601D` SoC only!
2. If your stick using ZTE chipset, this firmware are not compatible!

# 4-port Emulation
| Firmware                         | Mode | 4-port Emulation | Info |
|----------------------------------|------|------------------|------|
| `M110_sfp_ODI_210702.tar`        | HGU  | ❌ |  |
| `M110_sfp_ODI_220304.tar`        | SFU  | ✔️ |  |
| `M114_sfp_ODI_Vlan_220414.tar`   | SFU  | ✔️ |  |
| `M114_sfp_ODI_hybrid_220527.tar` | HGU  | ❌ |  |
| `M110_sfp_ODI_220817.tar`        | SFU  | ✔️ |  |
| `M110_sfp_ODI_220923.tar`        | SFU  | ✔️ | provided by [@lanseyujie](https://github.com/Anime4000/RTL960x/issues/24#issuecomment-1297975439) |
| `M114_sfp_ODI_hybrid_220916.tar` | HGU  | ❌ | provided by [@lanseyujie](https://github.com/Anime4000/RTL960x/issues/24#issuecomment-1297975439) |
| `M114_sfp_ODI_hybrid_221209.tar` (HSGQ) | HGU  | ❌ | provided by [@physx2494 ](https://github.com/Anime4000/RTL960x/discussions/148#discussioncomment-5802985) |
| `M110_sfp_ODI_240202.tar`        | SFU  | ✔️ |  |

# Checksum
| SHA256 | File name |
|--------|-----------|
| `b5e19fe71faa9f46cc6fbe911a73046dc8217a637063e86af785ed84cbe452c3` | M110_sfp_ODI_220817.tar |
| `e35f72dca3bb7f39be44167e0bb753f15f357ec4eb5345e8ce1e0d90179a38ab` | M110_sfp_ODI_220923.tar |
| `dd3741cbb8cb7926fdaa6386750453738dba773053a7090cc10c8018c7bb265d` | M114_sfp_ODI_hybrid_220916.tar |
| `94348FF82019562AB0D10814D307F5594BC8C4108676E196AA34FE1C413A3C15` | M114_sfp_ODI_hybrid_221209.tar |
| `50ccd3e6c77ca318ac9c0b2ee1cc1055c297acff480349ee68bab1ee829b0ced` | M110_sfp_ODI_240202.tar |

# HGD SFU Interchangable
If you upgrade IGD to SFU firmware or vice-versa, it's require to run factory reset via [erase `mtd3` partition](../../Docs/factory_reset.md#reset), then [generate new MAC KEY](../../Docs/Setup_Stick.md#dfp-34x-2c2-1) based on MAC Address that you want to set and reboot.

# `M110_sfp_ODI_220817.tar`
This firmware has custom fix and script, options are:

## Files
1. `fix_speed.sh` fix slow upload speed when using HiSGMII or 2500base-X
2. `fix_sw_ver.sh` allow custom software version when using `OMCI_OLT_MODE 3`
3. `fix_vlan_tag.sh` VLAN Tag Fix by @inyourgroove

## Activation
1. Enable `fix_speed.sh` execute `echo 1 > /etc/config/fix_speed` and `LAN_SDS_MODE` 4/5/6
2. Enable `fix_sw_ver.sh` require `OMCI_OLT_MODE 3` (custom software version)
3. Enable `fix_vlan_tag.sh` execute `echo 1 > /etc/config/fix_vlan`

> File `fix_sw_ver.sh` by @stich86 has upgraded, it will check `sw_custom_version0` & `sw_custom_version1` before apply, if empty, it will use `sw_version0` and `sw_version1` to prevent crash.

# SFU Mode
Switch Fabric Unit, ONU in Bridge Mode, Multiple VLAN, Internet provided by specific LAN Ports
![SFU](../../Docs/Images/xPON%20OMCI%20MIB%20SFU%20Mode.png)
If your ONU only in Bridge Mode, you need to use SFU firmware such as `M114_sfp_ODI_220304.tar`

# IGD Mode
Internet Gateway Device, ONU in Router Mode, ONU is Internet Gateway, having active DHCP, PPPoE Client, etc...
![IGD](../../Docs/Images/xPON%20OMCI%20MIB%20IGD%20Mode.png)
If your ONU has Wi-Fi, Internet, you need to use IGD firmware such as `M114_sfp_ODI_210702.tar`
