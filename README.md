# zfstm
ZFS backups to encrypted external drive

Inspired by TimeMachine, zfstm makes use zfSnap, cryptsetup and zxfer to create snapshots and copy them to an encrypted external drive. The tool will open, mount, take snapshot, replicate to external drive, then unmount and close LUKS volume at each run. Designed to run from cron with single parameter.

## Usage

	zfstm argument

### arguments

* hourly       = Open, mount, snapshot with 1d TTL, backup, unmount and close.
* daily        = Open, mount, snapshot with 1w TTL, backup, unmount and close.
* weekly       = Open, mount, snapshot with 1m TTL, backup, unmount and close.
* monthly      = Open, mount, snapshot with 1y TTL, backup, unmount and close.
* backup       = Backup external drive.
* mount        = Open and mount external drive.
* unmount      = Unmount and close external drive (ready to be unplugged).
* snapshot TTL = Take snapshot with TTK as time to live. 


## Setup

### Have a source ZFS pool

I assume you have one setup already.

### Have a destination ZFS pool over LUKS setup

Do something like this:

	sudo cryptsetup luksFormat -c aes-xts-plain64 -s 512 -h sha512 /dev/sdb
	sudo cryptsetup open --type luks /dev/sdb luks-myvoluuid
	sudo zpool create MYBACKUP /dev/mapper/luks-myvoluuid
  
### Use an OS that supports UUIDs to identify devices

Using UUIDs is required to recognize when the correct drive is plugged in.

### Add a keyfile to open and close encrypted LUKS volume available

Do something like

	sudo dd if=/dev/urandom of=/root/keyfile bs=1024 count=4
	sudo cryptsetup luksAddKey /dev/mapepr/luks-myvoluuid /root/keyfile

