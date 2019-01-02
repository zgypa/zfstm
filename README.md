# zfstm
ZFS encrypted backup to external drive

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

1. Have a source ZFS pool.
1. Have a destination ZFS pool over LUKS setup.
1. Use an OS that supports UUIDs to identify devices.
1. Add a keyfile to open and close encrypted LUKS volume available.


