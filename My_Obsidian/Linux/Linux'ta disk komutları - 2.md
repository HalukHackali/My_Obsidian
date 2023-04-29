#linux 
`
```
df -h
```
`
|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **Filesystem** | **Size** | **Used** | **Avail** | **Use%** | **Mounted on** |
| udev | 1.8G | 0   | 1.8G | 0%  | /dev |
| tmpfs | 379M | 11M | 368M | 3%  | /run |
| /dev/mmcblk1p1 | 15G | 6.7G | 7.3G | 48% | /   |
| tmpfs | 1.9G | 0   | 1.9G | 0%  | /dev/shm |
| tmpfs | 5.0M | 4.0K | 5.0M | 1%  | /run |
| /locktmpfs | 1.9G | 20K | 1.9G | 1%  | /   |
| tmp/dev/sda | 110G | 14G | 91G | 14% | /mnt/ssd |
| /dev/zram1 | 49M | 31M | 15M | 69% | /var/log |
| tmpfs | 379M | 0   | 379M | 0%  | /run/user/0 |

* * *

`
```
lsblk
```
`
|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| **NAME** | **MAJ:MIN** | **RM** | **SIZE** | **RO** | **TYPE** | **MOUNTPOINT** |
| sda | 8:0 | 0   | 111.8G | 0   | disk | /mnt/ssd |
| mmcblk1 | 179:0 | 0   | 14.6G | 0   | disk |     |
| └─mmcblk1p1 | 179:1 | 0   | 14.6G | 0   | part | /   |
| mmcblk1boot0 | 179:32 | 0   | 4M  | 1   | disk |     |
| mmcblk1boot1 | 179:64 | 0   | 4M  | 1   | disk |     |
| zram0 | 252:0 | 0   | 1.8G | 0   | disk | \[SWAP\] |
| zram1 | 252:1 | 0   | 50M | 0   | disk | /var/log |

* * *

```
~  du -sh * | sort -h

14G  ssd
```