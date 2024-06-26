# View Infortmation On Attached Device

```
udevadm info --query=all --name=/dev/nvme0n1p1
P: /devices/pci0000:00/0000:00:1d.0/0000:6e:00.0/nvme/nvme0/nvme0n1/nvme0n1p1
N: nvme0n1p1
S: disk/by-id/nvme-KXG60ZNV512G_NVMe_TOSHIBA_512GB_19PA303BK04N-part1
S: disk/by-id/nvme-eui.00000000000000018ce38e0300078219-part1
S: disk/by-partuuid/4076a2cb-01
S: disk/by-path/pci-0000:6e:00.0-nvme-1-part1
S: disk/by-uuid/010f1c08-bcd3-465f-9c49-7cd3522a7838
E: DEVLINKS=/dev/disk/by-uuid/010f1c08-bcd3-465f-9c49-7cd3522a7838 /dev/disk/by-partuuid/4076a2cb-01 /dev/disk/by-id/nvme-KXG60ZNV512G_NVMe_TOSHIBA_512GB_19PA303BK04N-part1 /dev/disk/by-id/nvme-eui.00000000000000018ce38e0300078219-part1 /dev/disk/by-path/pci-0000:6e:00.0-nvme-1-part1
E: DEVNAME=/dev/nvme0n1p1
E: DEVPATH=/devices/pci0000:00/0000:00:1d.0/0000:6e:00.0/nvme/nvme0/nvme0n1/nvme0n1p1
E: DEVTYPE=partition
E: ID_FS_TYPE=ext4
E: ID_FS_USAGE=filesystem
E: ID_FS_UUID=010f1c08-bcd3-465f-9c49-7cd3522a7838
E: ID_FS_UUID_ENC=010f1c08-bcd3-465f-9c49-7cd3522a7838
E: ID_FS_VERSION=1.0
E: ID_MODEL=KXG60ZNV512G NVMe TOSHIBA 512GB
E: ID_PART_ENTRY_DISK=259:0
E: ID_PART_ENTRY_FLAGS=0x80
E: ID_PART_ENTRY_NUMBER=1
E: ID_PART_ENTRY_OFFSET=2048
E: ID_PART_ENTRY_SCHEME=dos
E: ID_PART_ENTRY_SIZE=1000212480
E: ID_PART_ENTRY_TYPE=0x83
E: ID_PART_ENTRY_UUID=4076a2cb-01
E: ID_PART_TABLE_TYPE=dos
E: ID_PART_TABLE_UUID=4076a2cb
E: ID_PATH=pci-0000:6e:00.0-nvme-1
E: ID_PATH_TAG=pci-0000_6e_00_0-nvme-1
E: ID_SERIAL=KXG60ZNV512G NVMe TOSHIBA 512GB_19PA303BK04N
E: ID_SERIAL_SHORT=19PA303BK04N
E: ID_WWN=eui.00000000000000018ce38e0300078219
E: MAJOR=259
E: MINOR=1
E: PARTN=1
E: SUBSYSTEM=block
E: TAGS=:systemd:
E: USEC_INITIALIZED=1378820
```

# View Info On Device By Type

```
lsusb # list USB devices
lspci # list PCI (Peripheral Component Interconnect) devices
lsscsi # list SCSI devices
```

# Hard disk Nomenclature
```
/dev/hdd # First hard disk "a" # First hard disk "a"
/dev/hdd # Fourth hard disk "d"
/dev/hdd3 # Fourth hard disk "d", third partition
```

[Source](https://linuxjourney.com/lesson/udev)
