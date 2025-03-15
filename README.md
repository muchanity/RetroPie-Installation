# 🎮 **RetroPie Setup on a Dedicated Partition**

Transform your Raspberry Pi into the ultimate retro gaming console by setting up **RetroPie** on a dedicated partition for optimal performance and organization. Follow this pro guide to get everything up and running! 🚀

---

## 🛠️ **1. Check Available Partitions**

First, identify your partitions:

```bash
lsblk
```

Expected output:

```
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
nvme0n1     259:0    0 953.9G  0 disk 
├─nvme0n1p1 259:1    0   512M  0 part /boot/firmware
├─nvme0n1p2 259:2    0 553.4G  0 part /
└─nvme0n1p3 259:3    0   400G  0 part 
```

---

## 🔧 **2. Mount the Partitions**

Manually mount the partitions:

```bash
sudo mount /dev/nvme0n1p3 /storage/RetroPi
```

Verify the mount:

```bash
lsblk
```

Expected output:

```
└─nvme0n1p3 259:3    0   400G  0 part /storage/RetroPi
```

---

## 🔄 **3. Enable Auto-Mount on Boot**

Ensure the partitions are mounted at startup by editing `/etc/fstab`:

```bash
sudo nano /etc/fstab
```

Add these lines at the bottom:

```bash
/dev/nvme0n1p3  /storage/RetroPi  ext4  defaults  0 2
```

Save and exit (`CTRL + X`, then `Y`, then `ENTER`).

Test if everything mounts correctly:

```bash
sudo mount -a
```

If no errors appear, reboot:

```bash
sudo reboot
```

---

## 🕹️ **4. Install RetroPie on the Mounted Partition**

Navigate to the RetroPie mount location:

```bash
cd /storage/RetroPi
```

Clone the RetroPie setup repository:

```bash
git clone https://github.com/RetroPie/RetroPie-Setup.git
```

Set up permissions and install:

```bash
cd RetroPie-Setup
chmod +x retropie_setup.sh
sudo ./retropie_setup.sh
```
---

## 📂 **5. Relocate RetroPie to the Dedicated Partition**

Move the installation:

```bash
sudo mv /opt/retropie /storage/RetroPi
```

Create a symbolic link to maintain compatibility:

```bash
sudo ln -s /storage/RetroPi/retropie /opt/retropie
```

Move ROMs and configuration files:

```bash
sudo mv /home/mucha/RetroPie /storage/RetroPi
```

Create another symbolic link:

```bash
ln -s /storage/RetroPi/RetroPie /home/mucha/RetroPie
```

---

## ✅ **6. Final Steps & Launch**

Your **RetroPie setup** is now fully installed on a dedicated partition! To launch, simply run:

```bash
emulationstation
```

Enjoy your **RetroPie gaming experience** on an optimized setup! 🎮🔥

