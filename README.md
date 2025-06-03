# zfs-autosnap 
ZFS auto-snapshot script which runs before package upgrade using a libalpm (pacman) hook.

# Features
*  Creates ZFS snapshots before the system is updated using pacman, yay, or pamac. 
*  Deletes old snapshots based on a configurable retention parameter (maxSnapshots).
*  Can be manually executed by running `zfs-autosnap` command with elevated privileges.
*  Autosnaphot can be temporarily skipped by setting SKIP_AUTOSNAP environment variable (e.g. `sudo SKIP_AUTOSNAP= pacman -Syu`)

# /etc/zfs-autosnap.conf options:
*  `skipAutosnap` - if set to **true** script won't be executed.
*  `deleteSnapshots` - if set to **false** old snapshots won't be deleted.
*  `maxSnapshots` - defines **maximum** number of old snapshots to keep.
*  `snapshotDescription` - defines **value** used to distinguish snapshots created using timeshift-autosnap.
*  `rpool` - The pool and dataset that should be snapshotted before your pacman update. This should be set to your root dataset

# Notes
* I have kept compatibility with the original Timeshift script's configuration parameters, but I have changed the snapshot date format to match the one that is used by [sanoid](https://github.com/jimsalterjrs/sanoid).
* This snapshotting strategy works best on systems using [ZFSBootMenu](https://docs.zfsbootmenu.org/)
* Grub support for updating the snapshots in the boot menu should be possible, but is not included yet. 

# Future Ideas
* I'd like to see this script folded in to the Timeshift ecosystem via ZFS snapshot support in that tool, but still be usable alone.
* Expore whether we can integrate with or adapt this code into 

# Contribution
Your contribution is welcome - let me know what you're thinking about adding, or send a pull request, or fork this repo and release your own changes. 

# Prior Work
My adaptation of this codebase is a relatively minor contribution to FOSS. 

This work is based on the prior contributions of several others:

I found this prior art through Carlos Dagorret's github repository https://github.com/dagorret/timeshift-autosnap
This, in turn, was a clone of Matti Hyttinen's repository: https://gitlab.manjaro.org/Chrysostomus/timeshift-autosnap
Matti's work leveraged the extensive contributions of Marko Gobin: https://gitlab.com/gobonja/timeshift-autosnap as 
contributed to by [Hendrik Schöffmann](https://gitlab.com/gobonja/timeshift-autosnap/-/commit/a33da4c3f85b147d705c9af8c39e393760910092), 
[Rokosun](https://gitlab.com/gobonja/timeshift-autosnap/-/commit/42a582dde3478d9caac52e92cddde21a3e19e4a0), and 
[Pascal Jaeger](https://gitlab.com/gobonja/timeshift-autosnap/-/commit/0f933eb5966848d96477b5148e40ac1c3e750e22)

# Related work
The folks over at [Ditana Linux](https://ditana.org/) have done similar work, based on the same prior art. 
Their [zfs-autosnap AUR package](https://github.com/acrion/zfs-autosnap/tree/main?tab=readme-ov-file) is sublicensed under the
GNU AFFERO GENERAL PUBLIC LICENSE Version 3, which is more restrictive than the original MIT License that Marko Gobin used. 
While sublicensing MIT Licensed work as GPLv3 is legal and allowed, it's unusual. The original MIT License text and 
copyright is not referenced in Ditana's new license, which I think is problematic. That is 
the primary reason I have not deprecated this repository and continue to maintain it. 

For those folks that would like to install via the AUR and do not mind the licensing concerns I've outlined above, you 
may wish to check out Ditana's AUR package, which may have features you prefer.

