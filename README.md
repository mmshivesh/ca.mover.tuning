# Mover Tuning

## About

This is a simple [Unraid](https://unraid.net/) plugin that will let you fine-tune the operation of the [mover](https://docs.unraid.net/unraid-os/manual/additional-settings/#mover).

- On scheduled runs of mover
    - Only actually move file(s) if the the cache drive is getting full (selectable threshold)
    - Optionally don't move if a parity check / rebuild is already in-progress
- Optional ability to completely disable the scheduled runs of mover
- Manually executed runs of mover ("Move Now" button) can either follow the rules for schedules, or always move all files

This new fork merge all [pull requests](https://github.com/hugenbd/ca.mover.tuning/pulls) after review from [Hugenbd's repo](https://github.com/hugenbd/ca.mover.tuning) (cosmetics, merge skipfiletypes from shares, 4 changes from Swarles below) and add several feature, as for example automatic age threshold and compatibility with Unraid 7.x, and other stuff coming.

## How it works:

First it checks if it's valid for this script run: there must be a cache disk present and an instance of the script must not already be running.

Next, check each of the top-level directories (shares) on the cache disk.
For all share with 'Use Cache' setting set to "prefer" or "yes", we use 'find' to create a filtered file list of that share directory.
For all share with 'Use Cache' setting set to "only", we use 'du' or 'zfs list' to get total size of that share directory.

The list is sorted by "Use cache", increasing age, pool, and file inode, giving priority for being on cache to "cache only" shares, then "cache prefer" by moving newest from array to cache and older to array, and finally to "cache yes" share by moving only from cache to array.
Please note that if age setting is set to something else than "Auto (smart cache)" this script is actually dumb and do not check for size and free space and rely on your own calculations.
Files at the top level of the cache or an array disk (i.e not in a share) are never moved.

The list is then passed to original unraid mover.
For each file, if the file is not "in use" by any process (as detected by 'fuser' command), then the file is moved, and upon success, deleted from the source disk.  If the file already exists on the target, it is not moved and the sourceis not deleted.  All meta-data of moved files/directories is preserved: permissions, ownership, extended attributes, and access/modified timestamps.
If an error occurs in copying a file, the partial file, if present, is deleted and the operation continues on to the next file.

## Changelog
- 2024-07-30
    - [Various bug fixes](https://github.com/R3yn4ld/ca.mover.tuning/tree/2024-07-29-various-bug-fixes) [R3yn4ld](https://github.com/R3yn4ld) [Freender](https://github.com/freender)
    - [Enhance internal mover function](https://github.com/R3yn4ld/ca.mover.tuning/tree/enhance-processthemove-function) [R3yn4ld](https://github.com/R3yn4ld)

- 2024-07-29
    - [Automatic Array to Cache](https://github.com/R3yn4ld/ca.mover.tuning/tree/automatic-array-to-cache)
    - Complete rewrite of file listing functions (find, decide to move..) ([R3yn4ld](https://github.com/R3yn4ld))
    - [Fix an issue with inaccurate capacity when raid z1 is used](https://github.com/R3yn4ld/ca.mover.tuning/pull/9/) Updated zfs functions getting usage of a pool [Freender](https://github.com/freender)
    - Added cache mode "prefer" smart moving in "Automatic age" mode ([R3yn4ld](https://github.com/R3yn4ld))
    - Added option to "repair" Cache:Only (moving everything on share to cache) and Cache:No (moving everything on share to array) shares ([R3yn4ld](https://github.com/R3yn4ld))
    - Added option to synchronize Cache:Yes and Cache:Prefer shares to array so data are parity protected ([R3yn4ld](https://github.com/R3yn4ld))
    - Turbo write mode forcing improvement to not wake spinners if not needed ([R3yn4ld](https://github.com/R3yn4ld))
    - UI improvements ([R3yn4ld](https://github.com/R3yn4ld))

- 2024-07-10
    - [Unraid 7.0.0 compatibility](https://github.com/R3yn4ld/ca.mover.tuning/tree/unraid-7.0.0-compatibility) ([R3yn4ld](https://github.com/R3yn4ld)): original mover now works with "Move Now button follows plug-in filters" set to off - ([R3yn4ld](https://github.com/R3yn4ld))


- 2024-07-07:
    - [Unraid 7.0.0 compatibility](https://github.com/R3yn4ld/ca.mover.tuning/tree/unraid-7.0.0-compatibility) ([R3yn4ld](https://github.com/R3yn4ld))

- 2024-06-30: 
    - [Automatic age threshold](https://github.com/R3yn4ld/ca.mover.tuning/tree/automatic-age-threshold) ([R3yn4ld](https://github.com/R3yn4ld))
    - [Minor spelling corrections & README](https://github.com/dphelan/ca.mover.tuning/tree/spelling-corrections) ([Dphelan](https://github.com/dphelan))
    - [Merge share skipfiletypes](https://github.com/davendesai/unraid-mover-tuning/tree/merge-share-skipfiletypes) ([Davendsai](https://github.com/davendesai))(add/merge per share skipfilestype to global skips)
    - [Update Mover.tuning.page](https://github.com/Squidly271/ca.mover.tuning/tree/patch-2) ([Squid](https://github.com/Squidly271))

- 2023.12.19 (was not in [master branch from hugenbd](https://github.com/hugenbd/ca.mover.tuning))
    - [4 changes from Swarles](https://github.com/hugenbd/ca.mover.tuning/commit/64e06e91bd83431d768346e4d8158f7be039564e) ([Swarles](https://forums.unraid.net/profile/213067-swarles/))
        - Change "while read" lines in age_mover to "while IFS= read -r" to fix trailing white spaces (Swarles)
        - Fix where sometimes mover would not run to mover.old scrip (Swarles)
        - Log if "share.cfg" doesn't exists to help trouble shooting (Swarles)
        - Check for ca.mover.tuning.cfg file and additional logging. (Swarles)

## Installation

You can download and install plugins with [Community Apps](https://unraid.net/community/apps/c/plugins).

## Configuration

You'll find its settings within Settings - [Scheduler](https://docs.unraid.net/unraid-os/manual/additional-settings/#scheduler).

## Usage

After installation, the default settings are set so that there is no difference from Unraid's normal mover operations.

See the [_Mover Tuning_ thread on the Unraid support forum](https://forums.unraid.net/topic/70783-plugin-mover-tuning/) for more details and discussions.

## Thanks

This was originally created by [Squid](https://github.com/Squidly271) and updated by [hugenbd](https://github.com/hugenbd/ca.mover.tuning), with contributions by [Castcore](https://github.com/Castcore), [Swarles](https://github.com/hugenbd/ca.mover.tuning/commit/64e06e91bd83431d768346e4d8158f7be039564e), [Dphelan](https://github.com/dphelan) and [Davendsai](https://github.com/davendesai).
