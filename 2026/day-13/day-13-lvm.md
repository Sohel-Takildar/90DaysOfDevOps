# Day 13 – Linux Volume Management (LVM)

## Objective

Learn how to use Linux LVM (Logical Volume Manager) to create, manage, extend, and mount storage volumes dynamically.

---

# Step 1 – Switch to Root User

```bash
sudo -i
```

OR

```bash
sudo su
```

---

# Step 2 – Create a Virtual Disk (If No Spare Disk Available)

```bash
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024
```

## Attach the Disk

```bash
losetup -fP /tmp/disk1.img
```

## Verify Loop Device

```bash
losetup -a
```

Example Output:

```bash
/dev/loop0: []: (/tmp/disk1.img)
```

---

# Task 1 – Check Current Storage

## Commands Used

```bash
lsblk
pvs
vgs
lvs
df -h
```

## Purpose

* `lsblk` → Displays block devices
* `pvs` → Shows physical volumes
* `vgs` → Shows volume groups
* `lvs` → Shows logical volumes
* `df -h` → Displays mounted storage usage

---

# Task 2 – Create Physical Volume

## Command

```bash
pvcreate /dev/loop0
```

## Verify PV

```bash
pvs
```

Example Output:

```bash
PV           VG   Fmt  Attr PSize  PFree
/dev/loop0        lvm2 ---   1.00g 1.00g
```

---

# Task 3 – Create Volume Group

## Command

```bash
vgcreate devops-vg /dev/loop0
```

## Verify VG

```bash
vgs
```

Example Output:

```bash
VG         #PV #LV #SN Attr   VSize  VFree
devops-vg   1   0   0 wz--n-  <1.00g <1.00g
```

---

# Task 4 – Create Logical Volume

## Command

```bash
lvcreate -L 500M -n app-data devops-vg
```

## Verify LV

```bash
lvs
```

Example Output:

```bash
LV       VG         Attr       LSize
app-data devops-vg -wi-a----- 500.00m
```

---

# Task 5 – Format and Mount the Logical Volume

## Format the Volume

```bash
mkfs.ext4 /dev/devops-vg/app-data
```

## Create Mount Directory

```bash
mkdir -p /mnt/app-data
```

## Mount the Volume

```bash
mount /dev/devops-vg/app-data /mnt/app-data
```

## Verify Mount

```bash
df -h /mnt/app-data
```

Example Output:

```bash
Filesystem                         Size Used Avail Use% Mounted on
/dev/mapper/devops--vg-app--data  487M   24K  451M   1% /mnt/app-data
```

---

# Task 6 – Extend the Logical Volume

## Extend LV Size

```bash
lvextend -L +200M /dev/devops-vg/app-data
```

## Resize Filesystem

```bash
resize2fs /dev/devops-vg/app-data
```

## Verify Extended Size

```bash
df -h /mnt/app-data
```

Example Output:

```bash
Filesystem                         Size Used Avail Use% Mounted on
/dev/mapper/devops--vg-app--data  683M   25K  647M   1% /mnt/app-data
```

---

# Important LVM Components

| Component | Meaning         |
| --------- | --------------- |
| PV        | Physical Volume |
| VG        | Volume Group    |
| LV        | Logical Volume  |

---

# What I Learned

1. LVM provides flexible storage management in Linux.
2. Logical Volumes can be extended without recreating partitions.
3. Volume Groups combine multiple disks into a single storage pool.

---

# Challenges Faced

* Understanding the difference between PV, VG, and LV.
* Mounting the logical volume correctly.
* Resizing the filesystem after extending the LV.

---

# Conclusion

Today I learned how to create and manage storage using Linux LVM. I created a physical volume, volume group, logical volume, mounted it, and extended the storage dynamically without downtime.

---

# Git Commands Used

```bash
git add .
git commit -m "Completed Day 13 LVM Challenge"
git push origin main
```

---

# Screenshots to Capture

* `lsblk`
* `pvs`
* `vgs`
* `lvs`
* `df -h`
* `lvextend`
* `resize2fs`

---
