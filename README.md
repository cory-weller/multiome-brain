# multiome-brain

## Setting up GCP instance
Before starting, check which disk is to be mounted using `lsblk`.
In this example, `/dev/sdb` is to be mounted.

    NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
    sda       8:0    0   10G  0 disk 
    ├─sda1    8:1    0  9.9G  0 part /
    ├─sda14   8:14   0    3M  0 part 
    └─sda15   8:15   0  124M  0 part /boot/efi
    sdb       8:16   0   50G  0 disk 


```bash
# format the disk identified in the previous step.
sudo mkfs.ext4 -m 0 -E lazy_itable_init=0,lazy_journal_init=0,discard /dev/sdb
 
# create the target mount directory
sudo mkdir -p /mnt/data
 
# mount the disk to the directory
sudo mount -o discard,defaults /dev/sdb /mnt/data

# make read/writable for all users
sudo chmod a+w /mnt/data

# remove `lost+found`
rm -rf /mnt/data/lost+found
```

## Retrieve external files
```bash
# Install singularity
wget 'https://gist.githubusercontent.com/cory-weller/999ceb5dc7520e00ee84d0acce93a033/raw/6c386bfb1235a0d4a744f0d9c816ee763958d43e/gcloud-install-singularity.sh'
sudo bash gcloud-install-singularity.sh

# Retrieve test data
cd /mnt/data
wget -O multimodal-test-data.tar.gz 'https://onedrive.live.com/download?resid=77DD71E598E5B51B%2125139&authkey=!AGZwmo3mlJXQt3E'

# Retrieve singularity image
wget -O muon.sif 'https://onedrive.live.com/download?resid=77DD71E598E5B51B%2125138&authkey=!AJG4d9rDK7M-8iE'
```

