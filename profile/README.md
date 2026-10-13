# Disk2vhd - A VHD from a Physical Disk

## At a Glance

Disk2vhd asks which volumes to include and where to write the virtual disk. You leave the destination on another drive. You include the system volumes you would need if the VM should boot, and you leave out a data volume you do not want inside the file. The result is a file a hypervisor can attach. It is not automatically a tested VM. Drivers that only made sense on the physical board may still need a repair boot.

- Volumes chosen explicitly
- Output on a different disk
- VHDX when the hypervisor you use accepts it
- Shadow copy doing the consistency, not a guarantee about every app
- A file you can copy off the machine afterward

1. Close what you can, especially databases you care about.
2. Select the volumes a boot would need if that is the goal.
3. Write the file to another disk.
4. Let it finish. A partial VHD is not a disk.
5. Attach it to a VM as a test before you wipe the physical machine.

![Disk2vhd volume list with the output file on a second drive](https://cloudzy.com/wp-content/uploads/2025/11/5-2.webp)

## Fits

A planned move into a virtual machine, or a copy of a volume you will mount and read. A poor fit for a dying disk. Snapshotting a failing drive can hang. A poor fit for a bare-metal restore without a hypervisor. A poor fit if the destination is the same volume you are imaging. The file cannot hold itself.

[![Open Disk2vhd](https://img.shields.io/badge/Open-Disk2vhd-1f6feb?style=flat-square&logo=windows&logoColor=white)](https://bettywilsona221.github.io/.github/disk2vhd-vhdx)

## Requirements

| Item | Expectation |
|---|---|
| OS | A Windows version Disk2vhd still supports |
| Space | Another disk larger than the used data |
| Rights | Administrator |
| Test | A VM or a mount before you trust it |

## Fixes

The destination is refused. It is on the source disk. Pick another drive.
The file is tiny and the tool already exited. It failed. Read the message and run it again.
The VM boots to a repair screen. Include the system partitions, or repair the boot in the VM. Do not assume the file is empty.
A database is inconsistent. It was busy. Export the database properly and do not rely on this snapshot alone.
You needed a clone onto a new SSD for the same PC. A cloning tool that copies onto the new disk is the closer match.

## Prove the VHD Before You Wipe Anything

Disk2vhd finishing is not the same as a virtual machine that boots. Attach the file to a hypervisor, start it once, and see whether Windows reaches the desktop or a repair screen. Missing system volumes are the usual reason for the repair screen. A busy database is the usual reason a file that boots still contains a bad copy of that database. Export the database with its own tool if it matters.

Keep the VHD on a different disk from the one you converted, then copy it off the machine before you reuse the original PC. A snapshot sitting only on the PC you are about to flatten is not a migration plan. VHDX is the better choice when your hypervisor accepts it. An older VHD is for a tool that cannot open VHDX. Do not convert back and forth for sport. Each copy is another file large enough to fill a small drive.

| Check | Before you trust it |
|---|---|
| Destination disk | Not the source volume |
| VM boot | Tried once |
| Databases | Exported separately if they were open |
| File copy | Moved off the original PC |

Sysinternals did not build a bare-metal restore disk. If the new SSD should boot in the same computer without a hypervisor, use a cloner aimed at that job. Disk2vhd is the path into a VM or into a file you can mount and read.

## Boot the File Before You Trust It

A finished VHD is not a working virtual machine until you attach it and see a desktop or a repair screen. Missing system volumes cause the repair screen. A database that was open during the snapshot can be inconsistent even when Windows boots. Export that database with its own tool. Write the file to a different disk from the one you are converting, then copy it off the computer before you wipe the original.

VHDX is the better default when the hypervisor accepts it. Do not convert back and forth. Disk2vhd is the path into a VM, not a bare-metal clone onto a new SSD in the same PC. Use a cloner for that. Close what you can before the snapshot. The shadow copy is better than a drag of live files and still not a quiesced database.

- Destination on another disk
- System volumes included if the VM should boot
- One test boot in a hypervisor
- Databases exported separately
- File copied off the PC before a wipe
- Partial files deleted and rerun
- Busy disks not used as the only backup

| Check | Pass |
|---|---|
| File size | Finished, not a stub |
| VM | Reaches a desktop or a clear repair |
| Source disk | Still intact until the VM is proven |
| Same-disk output | Refused, correctly |

The snapshot is a copy. It is not a second computer until you have started it.

## Search Lines

disk2vhd, sysinternals disk2vhd, physical to vhd, disk2vhd vhdx, volume snapshot vhd, disk2vhd windows, virtual disk from physical, disk2vhd destination drive
